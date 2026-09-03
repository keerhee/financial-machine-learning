# Special Session — Building the AI-Native Asset Manager with LangGraph (Part 2)

*Financial Machine Learning · companion note to the navy deck · the implementation half of the AI-native asset manager session*

> Part 1 asked **what** an AI-native asset manager is and **why** it matters. This Part 2 answers **how**: we build the agent firm step by step in **LangGraph**, the graph framework purpose-built for multi-agent workflows. By the end you can sketch — and code — the firm from Part 1 yourself.

---

## 1. Why LangGraph fits this problem

In Part 1 we drew the firm as a diagram: agents in boxes, arrows between them, and a loop back from the risk agent. **LangGraph lets you write that exact diagram as code** — nodes, edges, and a shared state — then compile and run it. It models an agent workflow as an explicit **state machine**: each node is an LLM or a function, and edges define deterministic or agent-chosen transitions. That gives you observability and error handling that prompt-only agents rarely have.

What it provides:

- A shared, persistent **state** across the whole workflow.
- **Conditional routing and loops**, not just straight lines.
- Built-in **human-in-the-loop** and memory via a checkpointer.

It's mature, too — LangGraph reached 1.0, runs in production at firms like Uber, LinkedIn, and Klarna, and turns "prompt spaghetti" into a clear, auditable graph.

---

## 2. The three ideas: state, nodes, edges

That is the entire mental model.

- **State** — the shared notebook. One document that every agent reads and writes; the single source of truth (ticker, thesis, order, risk verdict, a running log).
- **Nodes** — the workers. Each node is just a function: it reads the state, does its job, and returns an update.
- **Edges** — the arrows. A **solid** edge always goes to the next node; a **conditional** edge runs a function that decides where to go — which is how you get branches and loops.

### Reducers — overwrite or append?

When two agents write to the state, who wins? A **reducer** decides. The default is overwrite (latest value wins), which is right for single facts like the current order. But for a **log** you want to *append* every entry, so you annotate the field with an "add" reducer:

```python
from typing import TypedDict, Annotated
import operator

class FirmState(TypedDict):
    ticker: str
    thesis: str            # filled by researcher
    order: int             # filled by trader
    risk_ok: bool          # filled by risk agent
    log: Annotated[list, operator.add]   # APPENDS, not overwrites
```

---

## 3. Building the firm — five steps

Every LangGraph app follows the same recipe: **define state → write nodes → wire edges → compile → run.**

### Step 2: the agent nodes

Each agent is a function with the same contract — state in, update out. Here the logic is simple rules; in a real system each node would call an LLM (the analyst with RAG over filings, the trader with the execution model, and so on).

```python
def analyst(state):
    view = 'bullish' if state['ticker'] else 'flat'
    return {'thesis': view, 'log': ['analyst: ' + view]}

def trader(state):
    size = 100 if state['thesis'] == 'bullish' else 0
    return {'order': size, 'log': ['trader: ' + str(size)]}

def risk(state):
    ok = abs(state['order']) <= 150        # a real limit
    return {'risk_ok': ok, 'log': ['risk: ' + str(ok)]}
```

### Step 3: wire the edges

```python
from langgraph.graph import StateGraph, START, END

g = StateGraph(FirmState)
g.add_node('analyst', analyst)
g.add_node('trader', trader)
g.add_node('risk', risk)

g.add_edge(START, 'analyst')      # always
g.add_edge('analyst', 'trader')
g.add_edge('trader', 'risk')
```

### Step 3b: the risk loop (conditional edge)

A conditional edge is a small function that returns the **name of the next node**. This single idea gives you loops and the risk veto: if risk says no, route back to re-debate; if yes, finish.

```python
def route_after_risk(state):
    if not state['risk_ok']:
        return 'analyst'          # VETO -> loop back to re-run
    return END                    # approved -> done

g.add_conditional_edges(
    'risk',                       # from this node
    route_after_risk,             # the decision function
    {'analyst': 'analyst', END: END},
)
```

### Steps 4–5: compile and run

Compiling validates the graph (every edge connects real nodes, no dead ends), and attaches a **checkpointer** that provides memory and the human-in-the-loop pause. After compile, the graph is locked and runnable.

```python
from langgraph.checkpoint.memory import MemorySaver

app = g.compile(checkpointer=MemorySaver())

start = {'ticker': 'AAA', 'log': []}
result = app.invoke(start, config={'configurable': {'thread_id': 'demo-1'}})

print(result['order'], result['risk_ok'])
for line in result['log']:
    print(' ', line)
```

> **The picture is the program.** The Part-1 firm diagram and this code are the same thing: `START → analyst → trader → risk`, with a conditional edge from `risk` that either loops back or ends.

---

## 4. Governance in the graph — human-in-the-loop

When an agent can act, a mistake becomes a real trade. So the human gate must be **compiled into** the graph, not bolted on. The mechanism is `interrupt_before`: the graph pauses before a node, the checkpointer saves the full state, a human reviews, and you resume exactly where it stopped.

```python
app = g.compile(
    checkpointer=MemorySaver(),
    interrupt_before=['execute'],   # pause before executing the trade
)

cfg = {'configurable': {'thread_id': 'demo-1'}}
app.invoke(start, config=cfg)       # runs, then PAUSES at 'execute'
# ... a human reviews the proposed trade (and can edit state) ...
app.invoke(None, config=cfg)        # RESUME after approval
```

Because the checkpointer persists state, a pause can last seconds or days and then resume with no lost work. That is what makes the system **governable**.

### Autonomy by risk level

We don't pause for everything — that would defeat the purpose. A conditional edge sends small, low-risk trades straight to execution and routes only large or hard-to-undo trades through the human gate. Fast where mistakes are cheap; careful where they are not.

### Observability

The `log` field already records every agent's action, and the checkpointer stores every state transition, so you can **replay** a run and read *why* a trade was made (Week 14 explainability). In practice, teams add tracing tools (LangSmith, Langfuse) and report much faster debugging. For production, swap `MemorySaver` for a database-backed checkpointer. A graph you can trace, pause, and replay is one a risk committee can actually sign off on.

---

## 5. Two common multi-agent patterns

- **Supervisor** — one manager node routes to specialist agents. The supervisor is, in effect, an agent whose tools are other agents. Simple, central control — our firm's fund manager. A great starting point.
- **Hierarchical teams** — each "agent" is itself a whole sub-graph (a team), e.g. an analyst team and a risk team with their own members. This composes small graphs into larger ones and scales to bigger firms without one giant graph.

Start with a supervisor; split into hierarchical teams only when a single graph gets unwieldy.

---

## 6. Hands-on labs

You can run the **full** version (`pip install langgraph langchain`, plug in any LLM) or the **toy** version where nodes are plain functions and no API key is needed. The graph structure is identical either way.

### Lab 1 — build and run the firm

```python
from langgraph.graph import StateGraph, START, END
# FirmState, analyst, trader, risk defined as above

g = StateGraph(FirmState)
for name, fn in [('analyst', analyst), ('trader', trader), ('risk', risk)]:
    g.add_node(name, fn)
g.add_edge(START, 'analyst'); g.add_edge('analyst', 'trader')
g.add_edge('trader', 'risk');  g.add_edge('risk', END)

app = g.compile()
out = app.invoke({'ticker': 'AAA', 'log': []})
print('\n'.join(out['log']))
```

### Lab 2 — risk loop and a human gate

```python
def route(state):
    return END if state['risk_ok'] else 'analyst'   # veto loops back

g.add_conditional_edges('risk', route,
                        {'analyst': 'analyst', END: END})

app = g.compile(checkpointer=MemorySaver(),
                interrupt_before=['execute'])
cfg = {'configurable': {'thread_id': 't1'}}
app.invoke({'ticker': 'AAA', 'log': []}, config=cfg)   # pauses
app.invoke(None, config=cfg)                            # resumes after approval
```

---

## 7. Taking it further

**Make the agents real:** swap each node's rules for an LLM with bound tools; give the analyst RAG over filings (Week 12), give the trader the execution model (Week 13), and add memory so agents recall past decisions.

**Make it production-ready:** swap `MemorySaver` for a database checkpointer, add tracing and evals (LangSmith/Langfuse), set hard limits and kill-switches on tools, and keep the human gates on every high-impact action.

The structure stays the same — same graph, bigger pieces.

---

## 8. Summary

1. **Model the firm as a graph.** State + nodes + edges. Each agent is a function; conditional edges create the risk loop and routing.
2. **Five steps, every time.** Define state, write nodes, wire edges, compile, run — the same recipe from a toy to production.
3. **Governance lives in the graph.** A checkpointer plus `interrupt_before` gives pause-approve-resume; loops, vetoes, and an audit trail come for free.

Part 1 was *what and why*; Part 2 is *how*. Together they describe a buildable, governable AI-native asset manager.
