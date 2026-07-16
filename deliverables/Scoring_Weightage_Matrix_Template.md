# Scoring Weightage Matrix — Reusable Template & Method

A general-purpose framework for turning a set of **criteria** into a
**weighted score** so you can rank, prioritise, or select between options
(questions, initiatives, vendors, candidates, features, risks — anything).

Copy this file into any project and adapt the criteria, weights, and scale.
Nothing here is specific to one project.

---

## 1. When to use this

Use a scoring weightage matrix whenever you need to make a **defensible,
comparable decision across multiple options** using **more than one factor**,
and those factors are **not equally important**.

Typical uses:

- Prioritising survey questions, features, or backlog items
- Ranking initiatives / projects for a portfolio
- Evaluating vendors, tools, or candidates
- Scoring risks (likelihood × impact is a special case of this)
- Shortlisting anything where "it depends on several things" is the answer

If every factor matters equally, you don't need weights — a simple average
is enough. Weights earn their keep when some criteria matter more than others.

---

## 2. Core concepts

| Term | Meaning |
|------|---------|
| **Option** | The thing being scored (a row in the final ranking). |
| **Criterion** | A factor you judge each option against (a column). |
| **Weight** | How important a criterion is, relative to the others. |
| **Score** | How well one option does on one criterion, on a fixed scale. |
| **Weighted score** | `score × weight`, summed across all criteria per option. |

**The formula**

```
Weighted score (option) = Σ ( score_i × weight_i )   for each criterion i
```

If your weights sum to 1 (or 100%), the weighted score lands on the **same
scale as your raw score** (e.g. 1–5), which makes results easy to read.

---

## 3. The five-step method

### Step 1 — Define the criteria
List the factors that genuinely drive the decision. Keep them:
- **Distinct** — avoid two criteria that measure the same thing (double-counting).
- **Few** — 4–7 is a sweet spot; more than ~8 dilutes and slows scoring.
- **Observable** — each should have a clear "what does a high vs low score look like".

### Step 2 — Assign weights
Decide how important each criterion is. Two common ways:

- **Direct allocation** — hand out 100 points (or a 0–1 share) across criteria.
- **Pairwise comparison** — compare criteria two at a time and derive weights
  (see §6). More rigorous, better when stakeholders disagree.

**Weights must sum to 100% (or 1.0).** Normalise if they don't (see §5).

### Step 3 — Set the scoring scale
Pick **one** scale and use it for every criterion. Common choices:

| Scale | Good for |
|-------|----------|
| 1–5   | General purpose, easy to reason about (default). |
| 1–3   | Quick triage (Low / Medium / High). |
| 0–10  | When you need finer separation between options. |

Write a short **rubric** so "4" means the same thing to everyone (see §4).

### Step 4 — Score every option against every criterion
Fill the matrix. Score each cell independently — judge the option on that
one criterion only, ignoring the others for the moment.

### Step 5 — Compute, rank, and sanity-check
Multiply, sum, rank. Then step back: does the ranking match intuition? If the
"obvious winner" lands mid-table, either your intuition or your weights are
wrong — investigate before trusting the number.

---

## 4. The matrix template

### 4a. Weight & rubric definition

| Criterion | Weight (%) | What a **low** score (1) looks like | What a **high** score (5) looks like |
|-----------|-----------:|--------------------------------------|---------------------------------------|
| Criterion A | 30 | … | … |
| Criterion B | 25 | … | … |
| Criterion C | 25 | … | … |
| Criterion D | 20 | … | … |
| **Total** | **100** | | |

### 4b. Scoring grid (raw scores, 1–5)

| Option | Crit A (30%) | Crit B (25%) | Crit C (25%) | Crit D (20%) |
|--------|:-----------:|:-----------:|:-----------:|:-----------:|
| Option 1 | 4 | 3 | 5 | 2 |
| Option 2 | 2 | 5 | 3 | 4 |
| Option 3 | 5 | 2 | 2 | 5 |

### 4c. Weighted result

Weighted score = Σ (raw score × weight). With weights as decimals
(30% → 0.30):

| Option | Calculation | Weighted score | Rank |
|--------|-------------|:--------------:|:----:|
| Option 1 | (4×.30)+(3×.25)+(5×.25)+(2×.20) | **3.60** | 1 |
| Option 2 | (2×.30)+(5×.25)+(3×.25)+(4×.20) | **3.40** | 2 |
| Option 3 | (5×.30)+(2×.25)+(2×.25)+(5×.20) | **3.50** | ~~?~~ |

> Recompute your own cells — the numbers above are illustrative. Because
> weights sum to 100%, the weighted score stays on the 1–5 scale, so **3.60
> reads as "3.6 out of 5"**.

---

## 5. Normalising weights

If your raw importance figures don't sum to 100, normalise:

```
normalised weight_i = raw weight_i / Σ (all raw weights)
```

**Example** — raw weights 3, 2, 2, 1 (sum = 8):

| Criterion | Raw | Normalised |
|-----------|:---:|:----------:|
| A | 3 | 3/8 = 0.375 |
| B | 2 | 2/8 = 0.250 |
| C | 2 | 2/8 = 0.250 |
| D | 1 | 1/8 = 0.125 |
| **Total** | **8** | **1.000** |

This lets you assign weights by feel ("A is 3× as important as D") and still
end up with a clean, comparable scale.

---

## 6. Deriving weights by pairwise comparison (optional, more rigorous)

When people can't agree on weights, don't argue about percentages — compare
criteria **two at a time**. It's easier to say "Is A more important than B?"
than "Is A worth 30%?".

1. Build a grid with every criterion as both a row and a column.
2. For each pair, mark the more important one (or score 1 = row wins,
   0 = column wins; use 0.5 for a tie).
3. Sum each row → that criterion's raw weight.
4. Normalise the row sums (§5) to get final weights.

| | A | B | C | D | Row sum | Weight |
|---|:-:|:-:|:-:|:-:|:------:|:------:|
| **A** | — | 1 | 1 | 1 | 3 | 0.375 |
| **B** | 0 | — | 1 | 1 | 2 | 0.250 |
| **C** | 0 | 0 | — | 1 | 1 | 0.125 |
| **D** | 0 | 0 | 0 | — | 0 | 0.000 |

> A zero weight means the criterion never won a comparison — consider dropping
> it, or use a softer scale (e.g. always give the winner 2 and loser 1) so
> nothing collapses to zero. This is a lightweight version of AHP (Analytic
> Hierarchy Process); use full AHP if you also need a consistency check.

---

## 7. Good practice & common pitfalls

**Do**
- Write the rubric **before** scoring, and score every option against it —
  not against each other.
- Keep criteria independent; merge any two that move together.
- Record **who** set the weights and **when** — weights are judgement calls
  and reviewers will ask.
- Run a quick **sensitivity check**: nudge the top weight up/down 10% and see
  if the ranking flips. If a small change reshuffles the winner, your decision
  is fragile — say so.

**Avoid**
- **Double-counting** — two criteria capturing the same underlying thing
  silently doubles its weight.
- **Reverse-scaled criteria** — for "cost" or "risk", either invert the score
  (low cost = high score) or label the column so higher always means better.
  Mixing directions within a matrix produces nonsense totals.
- **False precision** — a weighted score of 3.61 vs 3.60 is a tie. Treat
  near-ties as ties and break them with judgement, not decimals.
- **Set-and-forget weights** — revisit weights when the goal or context
  changes.

---

## 8. Quick-start checklist

- [ ] Listed 4–7 distinct criteria
- [ ] Assigned weights that sum to 100% (normalised if needed)
- [ ] Chose one scoring scale and wrote a rubric for it
- [ ] Confirmed every criterion is "higher = better" (inverted cost/risk)
- [ ] Scored each option against the rubric, one criterion at a time
- [ ] Computed weighted scores and ranked
- [ ] Sanity-checked the ranking and ran a sensitivity check
- [ ] Recorded who set the weights and when

---

## 9. Reproducible computation (optional Python)

Self-contained; needs only `pandas`. Swap in your own criteria, weights,
and scores.

```python
import pandas as pd

# 1. Weights (must sum to 1.0 — normalise if they don't)
weights = {"Crit A": 0.30, "Crit B": 0.25, "Crit C": 0.25, "Crit D": 0.20}
assert round(sum(weights.values()), 6) == 1.0, "Weights must sum to 1.0"

# 2. Raw scores per option (same scale for every criterion)
scores = pd.DataFrame(
    {
        "Crit A": [4, 2, 5],
        "Crit B": [3, 5, 2],
        "Crit C": [5, 3, 2],
        "Crit D": [2, 4, 5],
    },
    index=["Option 1", "Option 2", "Option 3"],
)

# 3. Weighted score = Σ (score × weight)
scores["Weighted score"] = scores.mul(pd.Series(weights)).sum(axis=1)
scores["Rank"] = scores["Weighted score"].rank(ascending=False).astype(int)

print(scores.sort_values("Weighted score", ascending=False).round(2))
```
