# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

This project builds a custom text classification pipeline using a fine-tuned transformer (`distilbert-base-uncased`) to categorize public gaming community posts. The classifier sorts community discussions into three distinct operational categories: empirical game mechanics and data analysis (`analysis`), provocative or emotional critiques (`hot-take`), and casual personal sentiment or reactions (`reaction`). By comparing a zero-shot baseline against our fine-tuned model across multiple random seeds, we evaluate how effectively fine-tuning captures nuanced gaming discourse.

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->



---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

## Label Taxonomy

### `analysis`

**Definition:** A post that evaluates specific checkable facts, quantitative metrics, frame data, statistics, or systematic performance comparisons.

**Example 1:**
> Looking at the frame data for this active skill, it has a 3-frame startup and is completely unsafe on block unless spaced properly at maximum range.

**Example 2:**
> I ran 50 consecutive test runs in the training arena to calculate the exact gold drop rate per hour, and it averages out to roughly 14,200 gold per zone.

### `hot-take`

**Definition:** A strongly opinionated, emotional, or provocative expression of frustration, praise, or general critique regarding game design or industry trends.

**Example 1:**
> This is literally the worst game ever made and anyone defending the developers has completely lost their mind.

**Example 2:**
> Multiplayer gaming peaked ten years ago and every single modern release is just a corporate cash grab designed to squeeze wallets.

### `reaction`

**Definition:** A personal expression of sentiment, casual commentary, or immediate emotional response to game events, updates, or character moments.

**Example 1:**
> So as I grew up I loved knights in armor I thought man there were the coolest people ever truly people who were broke and awesome the best and bravest Seeing halo for the first time...

**Example 2:**
> I genuinely cried when they unmasked the main character and threw away everything that made the lore special just to chase quick mainstream cash grabs.

### The hardest boundary

**Which two labels:** `analysis` and `hot-take`

**The decision rule I used every time:** 
> "If the post names a specific checkable fact, number, or empirical test, it's `analysis`, even if the tone is heated or critical."

### The hardest boundary

**Which two labels:** analysis and hot_take

**The decision rule I used every time:** If the post names a specific checkable fact, number, or empirical test, it's analysis, even if the tone is heated or critical.

<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->



---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:** Public gaming communities and discussion forums, focusing on empirical mechanics, frame data, narrative lore deep-dives, and passionate hot takes.

**How I labelled them:** I labelled the first 20 posts completely cold by hand to establish a clean baseline for consistency. The remaining 190 posts were pre-labelled using an AI assistant trained on my label definitions, after which I read, verified, and manually corrected every single one to ensure no noise or skimming errors entered the dataset.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| analysis | 70 | 20.4% |
| hot_take | 111 | 32.4% |
| reaction | 142 | 41.4% |
| **Total** | **323(active)** | **100%** |

**Three hard cases**

**1.**
> *The post:* "Looking at the frame data and patch notes, this character's startup is completely broken and ruins the entire competitive meta."
> *Could have been:* `analysis` or `hot-take`
> *I chose:* `hot-take`
> *Because:* Even though it references frame data and patch notes (which lean toward `analysis`), the dominant emotional tone and use of words like "completely broken" and "ruins" make it a heated `hot-take`.

**2.**
> *The post:* "I genuinely cried when they unmasked the main character and threw away everything that made the lore special just to chase quick mainstream cash grabs."
> *Could have been:* `reaction` or `hot-take`
> *I chose:* `reaction`
> *Because:* While it expresses strong frustration over industry trends, the deeply personal, narrative-focused emotional heartbreak fits squarely into a personal `reaction`.

**3.**
> *The post:* "I ran 50 consecutive test runs in the training arena to calculate the exact gold drop rate per hour, averaging 14,200 gold."
> *Could have been:* `analysis` or `hot-take`
> *I chose:* `analysis`
> *Because:* It relies entirely on empirical testing, numerical metrics, and systematic data gathering rather than emotional opinion.
---

## The Training Run

**Base model:** distilbert-base-uncased

**Settings:** epochs: 3, learning rate: 2e-5, batch size: 16, seed: 42

**Anything I changed from the defaults, and why:** Kept standard defaults for text classification fine-tuning (`distilbert-base-uncased`, 3 epochs, learning rate 2e-5) as they provide an optimal balance of fast convergence and stable generalization on small text datasets without overfitting.

**Split sizes:** 
Excluding 20 rows with missing labels, total active dataset is 323 rows, split as follows:
- **Train:** 225 rows
- **Val:** 49 rows
- **Test:** 49 rows

Per-label counts across splits:
| Label | Train | Val | Test |
|---|---|---|---|
| analysis | 49 | 10 | 11 |
| hot-take | 77 | 17 | 17 |
| reaction | 99 | 22 | 21 |


---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**
- *What I asked for:* Assistance in generating candidate label definitions and sorting initial gaming forum posts into structured categories.
- *What came back:* Drafted definitions for empirical posts vs. opinions.
- *What I changed:* Refined the definitions to establish strict boundaries (specifically adding the checkable-fact rule for `analysis` vs `hot-take`).

**Moment 2**
- *What I asked for:* Pre-labelling assistance for the bulk of the raw text dataset based on my finalized taxonomy rules.
- *What came back:* A batch of pre-assigned labels across the collected posts.
- *What I changed:* Read and verified every single pre-labelled row manually, correcting edge cases and misclassifications to ensure data integrity.

**Pre-labelling disclosure:** I used an AI assistant to pre-label the bulk batch of posts after manually annotating the first 20 cold. Every single pre-labelled row was subsequently reviewed, verified, and corrected by hand.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy | 0.347 | 0.531 | +0.184 |
| Macro F1 | 0.197 | 0.432 | +0.235 |
| F1 — `analysis` | 0.000 | 0.308 | +0.308 |
| F1 — `hot_take` | 0.500 | 0.286 | -0.214 |
| F1 — `reaction` | 0.091 | 0.702 | +0.611 |


**What I predicted before I looked:** I predict our fine-tuned model will beat the zero-shot baseline most notably on analysis and hot-take posts, because fine-tuning teaches the model our specific decision boundary for distinguishing empirical metrics from emotional complaints rather than relying on general zero-shot prompt associations.


<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
