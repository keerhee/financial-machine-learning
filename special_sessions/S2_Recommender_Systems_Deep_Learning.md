# Special Session — Recommendation Systems · Part 2 (Advanced / Deep Learning)

*Financial Machine Learning · companion note to the Part-2 navy deck*

> Part 1 covered the classics: content-based filtering, collaborative filtering, and matrix factorization. Part 2 climbs the ladder into **deep learning recommenders**, beginning with the crucial bridge — **Factorization Machines** — and ending at graph- and language-based models. Everything here recombines tools you already met: hidden factors (Week 9), neural nets (Week 8), attention and embeddings and LLMs (Week 12), and graph neural nets (Week 15).

---

## 1. Recap, and why we need more

Part 1 left us with matrix factorization: every user and every item gets a vector of hidden "taste dials," and a rating is the dot product of the two. It is elegant and scalable, but it hits a ceiling:

- It only knows **which user** and **which item** — it ignores context like age, time of day, or device.
- The dot product captures only **linear** taste.
- It has **no sense of order** — what you bought last carries no special weight.
- It strains on **huge, sparse, fast-moving catalogs.**

Deep learning lifts each of these ceilings. But we climb one rung at a time:

> **Matrix Factorization → Factorization Machine → DeepFM → deep recommenders (NCF, Two-Tower, SASRec, GNN, LLM).**

Each rung adds power: more features, then non-linearity, then sequence, graph, and language.

---

## 2. The bridge — Factorization Machines (FM)

The single most useful idea for understanding deep recommenders is the **Factorization Machine**. Where matrix factorization gives a hidden vector only to the *user ID* and the *item ID*, FM gives a hidden vector to **every feature** — user, item, age, time, device, anything — and then learns how every **pair** of features interacts.

$$
\hat{y} = w_0 + \sum_i w_i x_i + \sum_{i<j} \langle \mathbf{v}_i, \mathbf{v}_j \rangle \, x_i x_j
$$

Reading it: a baseline $w_0$; each feature's own weight $w_i$ (the linear part, like regression); and the key third term, where every pair of active features interacts, scored by the dot product of their hidden vectors $\langle \mathbf{v}_i, \mathbf{v}_j \rangle$.

Two facts make FM matter:

- **FM is a generalization of MF; MF is a special case of FM.** If the only features are the user ID and item ID, FM reduces exactly to matrix factorization. FM simply lets the same dial idea apply to *all* features.
- **It is efficient on sparse data.** Naively the pairwise term is $O(k \cdot n^2)$, but a standard rewrite reduces it to $O(k \cdot n)$ — linear time. That is why FM remains a backbone of large-scale ranking and click-through-rate systems even today.

### DeepFM — FM meets deep learning

Why choose between simple and deep? **DeepFM** runs an FM "wide" part and a neural-network "deep" part side by side, sharing the same input:

- **Wide (FM):** first- and second-order feature interactions.
- **Deep (MLP):** high-order, non-linear patterns.

The two outputs are combined for the final prediction. Compared to earlier wide-and-deep designs, DeepFM needs **no manual feature engineering** — it learns both low- and high-order interactions end to end. It became a workhorse for CTR prediction precisely because it is the natural fusion of the FM bridge with a deep net.

---

## 3. The deep recommenders

### 3.1 NCF — Neural Collaborative Filtering

NCF asks a simple question: why must the final step be a *dot product*? The dot product assumes taste is linear. NCF replaces it with a small neural network (MLP):

$$
\hat{r}_{u,i} = \text{MLP}\big( [\, \mathbf{u}_u \,\Vert\, \mathbf{v}_i \,] \big)
$$

We concatenate the user and item vectors ($\Vert$ means "glue together") and feed them through an MLP, which learns the curves and corners a dot product misses. In finance it is well suited to **implicit feedback** — bought vs. not bought, clicked vs. not — and it is the natural first deep step beyond matrix factorization.

### 3.2 Two-Tower — built for scale

When you must serve millions of customers against millions of items in real time, the **Two-Tower** model is the standard. It builds two separate neural networks:

$$
\text{score}(u, i) = f_{\text{user}}(u) \cdot g_{\text{item}}(i)
$$

- The **user tower** $f$ turns a user's features (age, history, goals) into a vector.
- The **item tower** $g$ turns an item's features into a vector.
- The match score is their dot product.

Why it scales: **item vectors are computed once and stored.** At request time only the user vector is fresh, and a fast nearest-neighbor search (e.g. Faiss) finds the top matches among millions of items in milliseconds. It is trained with **in-batch negatives** (contrastive learning, InfoNCE-style).

This fits the **two-stage** industrial system:

- **Stage 1 — retrieval:** Two-Tower narrows millions of items to a few hundred candidates.
- **Stage 2 — ranking:** a richer model (DeepFM, etc.) carefully orders the shortlist.

The towers themselves can embed sequences (SASRec/BERT4Rec) or graphs (PinSage), so the families combine.

### 3.3 SASRec — sequence-aware recommendation

Most recommenders treat your history as an unordered bag. But **order is signal**: opening a mortgage right after a home purchase points to *insurance* next. SASRec applies **self-attention** (the Week 12 Transformer idea) over a user's interaction *sequence* to predict the next item.

A neat property: SASRec adapts to data density. On **dense** histories it captures long-range dependencies like an RNN; on **sparse** histories it focuses on the most recent items like a Markov chain. Time-aware variants (**TiSASRec**) even use the gaps between events, not just their order. In finance this learns life-stage journeys such as *savings → fund → mortgage → insurance.*

---

## 4. The graph and language frontier

### 4.1 LightGCN — recommendation on a graph

Customers and products form a **bipartite graph**: a user links to every product they have used. A graph neural network (Week 15) lets each node refine its vector by absorbing its neighbors'. **LightGCN** strips the GNN down to its essentials — pure propagation, no heavy feature transforms or non-linearities:

$$
\mathbf{e}_v^{(k+1)} = \sum_{u \in N(v)} \frac{1}{\sqrt{|N(v)|\,|N(u)|}} \; \mathbf{e}_u^{(k)}
$$

A node's new vector is a normalized average of its neighbors' vectors, repeated over a few rounds so information spreads through the graph. LightGCN is **strong on sparse financial data** (most customers use few products), learns **high-order links** (friends-of-friends of products), and surfaces non-obvious cross-sell connections — all while being simple and stable to train.

### 4.2 ContextGNN and LLM-based recommendation

- **ContextGNN (ICLR 2025), "Beyond Two-Tower":** a hybrid that blends a Two-Tower retriever with a GNN, designed for **relational deep learning** over linked database tables. Its central argument is that **no single model wins everywhere** — real-world data needs a hybrid architecture.
- **LLM-based recommendation:** an LLM (Week 12) can both recommend and **explain in plain language** — *"Given your recent home purchase, consider mortgage insurance because..."* It handles cold-start gracefully using item descriptions. Its weakness is long interaction sequences, where dedicated models like SASRec still lead — so the two are often paired.

The pattern across the frontier: **combine specialists.** Retrieval, ranking, sequence, graph, and language each do one job well.

---

## 5. Which model for which job?

| Situation | Reach for |
|---|---|
| Many side features, sparse data, CTR prediction | Factorization Machine / DeepFM |
| Millions of items, real-time serving | Two-Tower (retrieval) + a heavier ranker |
| Order / life-stage matters | SASRec (sequence-aware) |
| Sparse customer-product graph | LightGCN / ContextGNN |
| Must explain *why* | LLM-based recommendation |

Start simple (FM), and add deep components only where they earn their keep — the same discipline as Week 1.

---

## 6. More power, same discipline

A deep recommender can overfit spectacularly and still look great in an offline test. Everything from Part 1 and Week 10 still applies — more so, because these models have more ways to fool you:

- **Split by time, not at random** — never let the model peek ahead.
- Evaluate with **precision@k / recall@k** on held-out data.
- Watch for **popularity bias** and **feedback loops** (the model recommends what it already favors).
- **Explain** recommendations and **check fairness** across customer groups (Week 14). Don't trap people in a narrow bubble of offers; keep a human in the loop for high-stakes decisions.

The stakes in finance are someone's savings, so honesty and fairness matter even more than raw accuracy.

---

## 7. Hands-on labs

Tiny inline demos — built to reveal the mechanism, not to train a production model.

### Lab 1 — Factorization Machine score

Each feature gets a small hidden vector; the score sums a baseline, each feature's weight, and every pairwise interaction.

```python
import numpy as np
x = np.array([1.0, 1.0, 0.0])            # active features
w0, w = 0.1, np.array([0.2, -0.1, 0.3])  # bias + linear weights
V = np.array([[0.5, 0.1],                # hidden vector per
              [0.2, 0.4],                #   feature (k=2)
              [0.9, 0.0]])

linear = w0 + w @ x
inter = sum((V[i] @ V[j]) * x[i] * x[j]
            for i in range(3) for j in range(i + 1, 3))
print('FM score:', round(linear + inter, 3))
```

### Lab 2 — Two-Tower matching

One user-tower vector, several item-tower vectors; score by dot product and recommend the best.

```python
import numpy as np
# user tower output (one vector)
user = np.array([0.8, 0.2, 0.5])
# item tower outputs (one row per fund)
items = np.array([[0.7, 0.1, 0.6],   # fund 0
                  [0.1, 0.9, 0.0],   # fund 1
                  [0.9, 0.0, 0.4]])  # fund 2

scores = items @ user                # dot-product match
best = scores.argmax()
print('match scores:', scores.round(2))
print('recommend fund', best)
```

Then scale up with a real library (RecBole, LibRecommender) on a public ratings dataset.

---

## 8. Summary

1. **Climb the ladder, don't leap.** MF → FM → DeepFM → deep. FM is the bridge: the same hidden-dial idea, extended to every feature, learning all pairwise interactions — and MF is just a special case of it.
2. **Each deep model has a job.** NCF for non-linearity, Two-Tower for scale, SASRec for sequence, LightGCN/ContextGNN for sparse graphs, and an LLM when you must explain.
3. **More power, same discipline.** Split by time, evaluate honestly (Week 10), explain and stay fair (Week 14). Deeper models have more ways to fool you.

Part 1 and Part 2 together take recommendation from the classics to the frontier.
