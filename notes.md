# Candidate distinctions for r/gaming

> Drafted with Claude before reading (Claude couldn't access Reddit). Check each
> against my own 30–40 posts and replace the example lines with real ones.

## 1. Some posts give a specific, checkable detail. Most don't.

Some comments name something you could verify: hours played, price, frame rate,
a patch number, a release year, a mechanic by name. Most just state a verdict.

- "I'm 60 hours into it and the late-game crafting loop still hasn't changed since hour 10."
- "This game is mid."

## 2. Some posts are about the writer's own experience. Others make a claim about games in general.

"I" posts report what happened to the writer: they finished a game, got
frustrated, a game meant something to them. Claim posts say something about the
world, such as an industry trend or a game being overrated.

- "Just beat the final boss after three days of trying, my hands are shaking."
- "Open-world games have all become checklist simulators."

## 3. Some posts compare two named things. Others judge one thing alone.

Comparison posts give the reader a point of reference ("plays like X but with
Y"). Standalone verdicts don't.

- "The combat is basically Dark Souls with a dodge-cancel, which makes it way more forgiving."
- "The combat sucks."

## 4. Some posts give a reason. Others just assert.

This test is looser than #1: does the post contain a "because" (stated or
implied), even without a checkable fact?

- "I dropped it because every side quest is a fetch quest with a different skin."
- "Worst game of the year, not even close."

## How these map to labels

- #1 and #4 overlap. #1 is the strict version (a checkable fact) and #4 is the
  loose version (any reason). Choosing between them is the decision rule for my
  hardest boundary.
- #2 separates a reaction-type label from a claim-type label.
- #3 is probably a signal within the more substantial label, not a label on its own.
- A natural three-label setup would be substantiated claim / bare claim /
  personal reaction. That's close to the staff taxonomy, which is fine.

## Real posts so far

- Halo TV show / Master Chief helmet post (in `labels.csv`). It's long and
  emotional and about the writer's childhood, but it also makes a general claim
  ("money grubbing", "intentionally trying to ruin halo"). That puts it on the
  #2 boundary, so it's a hard-case candidate.

---

## Glossary

- **Label:** The category you assign to one post. analysis, hot_take, and so on.
- **Taxonomy:** Your whole set of labels, plus the rules for choosing between them.
- **Annotation:** The act of assigning labels by hand. Also called labeling.
- **Class imbalance:** When one label covers most of your data. A model trained on it learns to guess that label.
- **Fine-tuning:** Taking a model that already knows language, and teaching it your specific distinction.
- **Epoch:** One full pass of your training data through the model. Three is a normal number.
- **Held-out set:** Examples the model never trained on. The only honest place to measure it.
- **Leakage:** When held-out examples sneak into training. It makes scores look great and mean nothing.
