# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1. Overall Accuracy

<!-- Your criterion. It must name a number. -->
Criterion: The overall classification accuracy on the held-out test split is at least 0.70 across all three seeds.




**Why this target:**
With three evenly balanced classes, a random baseline sits at 33.3%. Given that our dataset of 210 examples provides about 70 instances per class, a 70% overall accuracy threshold requires the model to correctly identify roughly 22 out of 31 test examples, ensuring it captures the distinct textual boundaries between emotional rants, technical instructions, and promotional marketing.


---

## 2. Per-Label Performance

<!-- Your criterion. -->
Criterion: Every individual label achieves an F1 score of at least 0.60 on the held-out set across all three seeds.


**Why this target:**
Because our test split contains only about 10 examples per label, individual class F1 scores can fluctuate easily between seeds. Setting the floor at 0.60 accounts for this small-sample variance while ensuring that no single category (such as narrative_rant or promotional_post) is completely ignored or misclassified by the model.


---

## 3.

<!-- Your criterion. -->

Criterion: No single predicted label accounts for more than 50% of the model's total predictions on the test set.



**Why this target:**



---

## 4. Consistency

<!-- Your criterion. -->

When evaluating model predictions across three different random seeds (42, 7, 2024), the macro F1 score standard deviation remains under 0.08.

**Why this target:**

Training transformers on small datasets (210 rows) can lead to high variance depending on weight initialization and data shuffling. A standard deviation under 0.08 ensures that our performance is stable and reproducible rather than being an artifact of a single lucky seed.

---

## 5. Confidence

<!-- Your criterion. -->

Criterion: Predictions where the model's softmax confidence score is greater than 0.80 achieve an accuracy of at least 0.85.

**Why this target:**
A well-calibrated classifier should be more accurate when it is certain. Requiring high-confidence predictions to be correct at least 85% of the time verifies that the model's internal probability outputs are meaningful rather than overconfident guesses on ambiguous boundary cases.


---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
