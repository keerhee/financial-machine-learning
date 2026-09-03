# Special Session — Recommendation Systems

*Financial Machine Learning · companion lecture note to the navy deck*

> The third "running app" of this course — fraud detection and the finance chatbot got full weeks; here recommendation gets its own special session. Almost everything below is built from tools you already met: cosine similarity (Week 12), PCA (Week 9), embeddings (Week 12), and honest evaluation (Week 10).

---

## 1. What is a recommender?

A recommender is the smart shop assistant who remembers what everyone likes. Netflix suggests your next show, Amazon your next purchase, Spotify your next song. In every case the system does the same job: given who you are and what you have liked, predict what you will like next, then suggest the items with the highest predicted score.

Formally, imagine a giant table of ratings where rows are users and columns are items. Most cells are blank — nobody has rated most things. A recommender's job is to **fill in the blanks**: estimate the rating you would give an item you have not seen, then recommend the items with the highest estimates.

**Why finance cares.** The same machinery decides which fund, card, loan, or insurance product to offer a client ("next best action"), drives cross-selling, personalizes the app, and powers robo-advisors that match portfolios to people. The engine is the same as Netflix's; the difference is that the stakes are someone's savings, so honesty and fairness matter more.

There are two big families of recommender, and most real systems blend both:

| Family | Matches by | Strength | Weakness |
|---|---|---|---|
| Content-based | the **item's features** | works with few users; explains itself; no cold-start for new items | stays in a bubble of look-alikes; needs clean features |
| Collaborative filtering | the **pattern of who liked what** | finds surprising picks; needs no item features | needs many users; cold-start for new users/items |

---

## 2. Content-based filtering — recommend by the item

The idea: describe each item by its **features** (genre, spice level, risk, sector, price...), then recommend items whose features are close to what you already liked. *You liked a spicy ramen, so here is a spicy curry.* No other users are needed — only the item descriptions and your own history.

"Close" is measured with the same **cosine similarity** from Week 12 — the angle between two feature vectors:

$$
\text{similarity} = \cos(\theta) = \frac{a \cdot b}{\lVert a\rVert \, \lVert b\rVert}
$$

A value near $1$ means the two items point the same way (very similar); near $0$ means unrelated.

**Strengths.** No cold-start for a brand-new item, because we can use its features immediately. Easy to explain: "recommended because both are spicy."

**Limits.** It can trap you in a bubble — it only ever suggests look-alikes of things you already chose, never a pleasant surprise. And it lives or dies by the quality of the feature data.

---

## 3. Collaborative filtering — recommend by the people

Collaborative filtering ignores *what the items are*. It looks only at the **pattern** of who liked what. If you and Mia agree on Funds A and B, and Mia also loves Fund C that you have not tried, then Fund C is a strong recommendation for you. It is the wisdom of similar people.

There are two flavors:

- **User-based:** find users whose ratings look like yours, then recommend what those neighbors liked. Intuitive, but slow with millions of users.
- **Item-based:** find items that tend to be rated together; if you liked $X$, suggest items often liked alongside $X$. This is the "frequently bought together" you see on shopping sites — usually faster and more stable in practice.

Both rely on a similarity measure (cosine again). The trouble is scale and sparsity: with millions of users and items, and almost every cell blank, raw neighbor-search struggles. The fix is matrix factorization.

---

## 4. Matrix factorization — hidden taste factors

The breakthrough idea (famous from the Netflix Prize) is that a giant, mostly-blank ratings table can be **approximated by a few hidden "taste dials."** Perhaps taste really comes down to a handful of factors — *likes risk?, likes tech?, likes income?* Each user has a setting on each dial; so does each item. Multiply them together and you can predict any blank cell.

$$
R \approx U \, V^{\top}
$$

Here $R$ is the ratings table, $U$ holds each user's hidden dials, and $V$ holds each item's dials. To predict a single rating, take the dot product of that user's vector and that item's vector:

$$
\hat{r}_{u,i} = \mathbf{u}_u \cdot \mathbf{v}_i
$$

This should feel familiar. Discovering a few hidden factors that explain a big table is **exactly the PCA idea from Week 9**, and the user/item vectors are **embeddings, just like Week 12**. You already understand the machinery — it is being pointed at a ratings table instead of stock returns or words.

---

## 5. The cold-start problem

Collaborative filtering needs history. A **brand-new user** has rated nothing, so there is no pattern to compare; a **brand-new item** has no ratings either. The assistant has nothing to go on. This is the cold-start problem.

Common fixes:

- Fall back to **content-based** filtering (use item features, which exist from day one).
- Ask a few **onboarding questions** to seed a profile.
- Recommend **popular items** to start.
- Use whatever you already know — age, stated goals, region.

Then switch to collaborative filtering as the user's history grows. In practice, hybrids that combine both families handle cold-start gracefully.

---

## 6. Evaluating a recommender honestly

It is just as easy to fool yourself here as with a trading backtest (Week 10). If you test the model on ratings it already saw during training, it will look brilliant and then fail on real new users. The cure is the same: **hide some real ratings, predict them, and check the hits — always on data the model never saw.**

A common metric is **precision@k**: of the top $k$ items you recommend, how many did the user actually like? But accuracy is not everything. A good recommender also cares about:

- **Diversity** — don't show ten near-identical items.
- **Novelty** — surface things the user would not have found alone.
- **Fairness** (Week 14) — don't trap groups in narrow bubbles or amplify bias.

---

## 7. Recommenders in finance

- **Product & cross-sell:** suggest the next card, loan, or insurance; "next best action" per client; personalized offers.
- **Robo-advisor:** match portfolios to a client's goals and risk; recommend funds similar to ones they hold; blend content (fund features) with collaborative signals.
- **Research & news:** surface filings and news like the ones a user reads; recommend stocks similar to a watchlist — which connects directly to embeddings and RAG from Week 12.

---

## 8. Hands-on labs

Build a tiny ratings matrix right in the notebook — rows are users, columns are funds, zeros mean "not rated yet":

```python
import numpy as np
# rows = 4 users, cols = 5 funds; 0 means 'not rated yet'
R = np.array([[5,4,0,0,1],
              [4,0,0,2,1],
              [1,1,0,5,4],
              [0,0,5,4,4]], float)
```

### Lab 1 — item-similarity recommender (content / item-based)

Treat each fund (column) as a vector of ratings and find the most similar fund to one a user liked.

```python
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity

# items are columns -> compare funds by their rating columns
item_sim = cosine_similarity(R.T)   # fund-by-fund similarity
np.fill_diagonal(item_sim, 0)       # ignore self-match

liked = 0                           # user liked fund 0
best = item_sim[liked].argmax()
print('you liked fund', liked)
print('most similar fund to recommend:', best)
```

### Lab 2 — matrix factorization (fill the blanks with SVD)

Factor the ratings into a few hidden dials, then multiply back to predict every cell, including the blanks.

```python
import numpy as np
from sklearn.decomposition import TruncatedSVD

svd = TruncatedSVD(n_components=2, random_state=0)
U = svd.fit_transform(R)            # user dials
V = svd.components_                 # item dials

R_hat = U @ V                       # predicted full ratings
user = 0
unseen = np.where(R[user] == 0)[0]  # funds not yet rated
pick = unseen[R_hat[user, unseen].argmax()]
print('recommend fund', pick, 'to user', user)
```

Then swap in a bigger ratings matrix and watch how the suggestions change.

---

## 9. Summary

1. **Two families, often blended.** Content-based matches by item features; collaborative filtering matches by the pattern of who liked what. Hybrids combine their strengths.
2. **Matrix factorization is the workhorse.** Discover a few hidden taste factors and multiply to predict the blanks. It is PCA and embeddings applied to a ratings table.
3. **Test honestly, recommend responsibly.** Hide ratings to evaluate (precision@k, no leakage), and value diversity and fairness — not just raw accuracy.

This completes all three running apps of the course: **fraud detection, the finance chatbot, and recommendation.**
