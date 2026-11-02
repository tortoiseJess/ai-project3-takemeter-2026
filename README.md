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

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->

Google reviews of restaurants in Santa Clara California, focusing on Japanese restaurants.
Classifer sorts posts into 
1. positive: will go again, highly recommended by reviewer. 
2. Neutral, reviewer have both negaitve and positive comments or recommend others to go if have don't mind some trade offs or really craving a dish.
3. negative: Will not go again, had a poor experience.


---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `Positive`

**Definition:**
positive: customer explicitly expresses intent to go again or positive comments dominate in cases where no such comment was expressed.

**Example 1:**
>Probably one of the first customers here since they just opened and there were almost no reviews when I came, so I honestly kept my expectations pretty neutral.

After dining here, I was surprised by how polished everything already felt. It didn’t feel like a newly opened place still figuring things out.

Sitting at the counter was a great experience — you can watch the chef prepare and serve each course, and the pacing felt smooth and relaxed. No rushing, no trying too hard to create a luxury atmosphere, just a comfortable and focused dining experience.

The omakase itself had a nice flow. From appetizers to sashimi, warm dishes, and finally the nigiri, each course transitioned naturally and didn’t feel repetitive. A few pieces of nigiri really stood out — the fish quality was excellent and the rice was balanced without overpowering the flavor. I especially enjoyed the seared course and some of the tuna selections.

One thing that surprised me: the portion was actually very satisfying. I expected a typical fine dining omakase where you leave wanting more, but this was a full meal and I left genuinely full — not because of extra rice, but because the pacing and portions were thoughtfully done.

Since the restaurant is brand new and doesn’t have many reviews yet, I hope they can keep this level of quality consistently.

Would definitely come back

**Example 2:**
>Had an amazing all-you-can-eat Wagyu hot pot experience here! The quality of the meat was excellent — beautifully marbled, tender, and incredibly flavorful. Every plate came out fresh, and it was hard to stop ordering more.

The broth was rich and delicious without overpowering the ingredients, and there was a great variety of vegetables, sides, and sauces to choose from. Everything felt high quality and well maintained.

The service was attentive, and orders arrived quickly throughout the meal. For anyone who loves Wagyu and hot pot, this place is absolutely worth a visit.

Definitely one of the better AYCE hot pot spots I’ve been to, and I’ll be coming back for sure! 🍲🥩✨

### `Negative`

**Definition:**
negative: Will not go again is expressed by customer.
**Example 1:**
>"I really like the concept as a person who was brought up in Tokyo ie part conbini, osouzaiya, deli.  I have several minor issues with their food quality though.  Ordered deluxe okonomiyaki which was closer to Hiroshima style with noodles, but the noodles were hard.  Crunchy hard.  And way, way too much mayo .  All I could taste was mayo.  Sickening amount of mayo spread on it.

Next item I purchased was 5 pieces of oinarisan ie stuffed deep fried tofu skin with different topping. Topping was generally ok, except few pieces slathered with too much mayo again. Go easy on mayo and they would be better."

**Example 2:**
>Came here for lunch. Nearly empty restaurant but we sat with our menus waiting for service for 15 minutes. The woman who seated us and gave us our menus took the food order from a guest who arrived after us and then completely ignored us while she went to fold napkins and set up empty tables. We were no longer looking at our menus and kept trying to make eye contact with her. We got up and left so I’m sorry I don’t know how the food is.


### `Neutral`
**Definition:**
neutral: reviewer have equal amount of negaitve and positive comments or recommend others to go if have don't mind some trade offs or really craving a dish.
**Example 1:**
>"We had 4 dishes and a pot of oolong tea.  Tea was not strong which was good for night time 😊.  Sashimi 3 kinds was fresh, but thin slices.
Crispy chicken skin was pretty good. Dipping it with the sauce gave different flavor but made it less crispy.  I preferred having the crispy chicken skin without sauce.
Squid was a bit salty.  The pork belly skewer was quite special flavor - tasty!
Lychee sorbet was really good! It had a bit touch of yuzu to me… Highly recommend it.  It refreshed the mouth😋😋😋

Staff were very friendly and nice.  Service was quick.  The restaurants was pretty clean and not crowded with the table setting.  It was busy but the level of noise was acceptable until a group of people came in.🤪

I recommend this restaurant for people are not looking for sushi rolls"

**Example 2:**
>"KOKO Izakaya & Oyster House was a good spot for a quick Sunday lunch, especially if you’re craving sushi. The restaurant was quite busy, which created a lively atmosphere. We ordered a few sushi rolls, miso soup, and seaweed salad. While the presentation wasn’t particularly impressive, the food was fresh and met our expectations. The miso soup was simple but comforting, and the kids really enjoyed it. The seaweed salad was fresh, and the sushi tasted good with generous portions of fish.

The service was decent overall, although we had to get our server’s attention a few times since he wasn’t checking in on our table very often. It wasn’t a bad experience, but a little more attentiveness would have made the meal more enjoyable.

Overall, if you’re looking for a casual place to satisfy a sushi craving without expecting anything fancy, KOKO Izakaya & Oyster House is worth a visit. The food was enjoyable, the restaurant had a nice atmosphere despite being busy, and we’d consider stopping by again when we’re in the area."

### The hardest boundary

**Which two labels:**
positive vs neutral or negative vs neutral
**The decision rule I used every time:**
<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->
if reviewer explicity says will go again , then label is positive
if reviewer explicty says will not go again  then label is negative
if they recommend people to go for a specific reason or craving or don't mind some trade offs. 
If no such comment is mentioned, then count postive comments and negative comments and if they are equal, label is "neutral"
more positive comments then negative --positive, (more negative comments, then label is negative)

---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**
Google reviews from google maps platform.
**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->

I labelled first 43 and collected them from google reviews.
I gave criteria to AI and asked it to 1. collect the rest using a scraper script.
2. label for me with a reason and evidence sentence.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| positive | 84 | 44.7% |
| negative | 54 | 28.7% |
| neutral | 50 | 26.6% |
| **Total** |188  | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:*
>>"We had 4 dishes and a pot of oolong tea.  Tea was not strong which was good for night time 😊.  Sashimi 3 kinds was fresh, but thin slices.
Crispy chicken skin was pretty good. Dipping it with the sauce gave different flavor but made it less crispy.  I preferred having the crispy chicken skin without sauce.
Squid was a bit salty.  The pork belly skewer was quite special flavor - tasty!
Lychee sorbet was really good! It had a bit touch of yuzu to me… Highly recommend it.  It refreshed the mouth😋😋😋

Staff were very friendly and nice.  Service was quick.  The restaurants was pretty clean and not crowded with the table setting.  It was busy but the level of noise was acceptable until a group of people came in.🤪

I recommend this restaurant for people are not looking for sushi rolls"
> *Could have been:*
positive
> *I chose, because:*
There was an explicity statement recommend parties other than the reviewer herself that didn't mind the tradeoffs of not having sushi rolls
**2.**
> *The post:*
"I really like the concept as a person who was brought up in Tokyo ie part conbini, osouzaiya, deli.  I have several minor issues with their food quality though.  Ordered deluxe okonomiyaki which was closer to Hiroshima style with noodles, but the noodles were hard.  Crunchy hard.  And way, way too much mayo .  All I could taste was mayo.  Sickening amount of mayo spread on it.
Next item I purchased was 5 pieces of oinarisan ie stuffed deep fried tofu skin with different topping. Topping was generally ok, except few pieces slathered with too much mayo again. Go easy on mayo and they would be better."
> *Could have been:*
neutral
> *I chose, because:*
negative , because negative comments dominated.
**3.**
> *The post:*
>"We have been here probably 10 times and it’s always such an interesting and delicious experience!
 The nigiri is always cut beautifully.
 The chawanmushi and desserts change seasonally.
 Sake options are great.
 We always sit at the bar and sometimes we get some special cuts or some experimental dishes from the chef which always makes our night so much more fun!"
> *Could have been:*
>neutral
> *I chose, because:*
positive because positive comments dominated.
---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:** distilbert-base-uncased (the notebook default)

**Settings:** 3 epochs, learning rate 2e-5, batch size 16, seed 42, max length 128 tokens

**Anything I changed from the defaults, and why:** Nothing. I kept the notebook defaults as a baseline before tuning anything.

**Split sizes:** 130 train / 29 val / 29 test (188 labelled posts), stratified split.

| Label    | Train | Val | Test |
|----------|-------|-----|------|
| Positive | 56    | 10  | 18   |
| Negative | 35    | 12  | 7    |
| Neutral  | 38    | 7   | 4    |

Negative has only 7 test examples and Neutral has only 4. Both are under the ~8 cutoff, so metrics on those labels will swing a lot between seeds. That is a limit of the test set, not necessarily a problem with the model.



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:* How to fill in the Training Run section of the README (the model, settings, changes from defaults, and split sizes).
- *What came back:* A draft pulled from my notebook and results.json: distilbert-base-uncased, 3 epochs, lr 2e-5, batch 16, seed 42, and a 130/29/29 split with per-label counts, noting that Negative (7) and Neutral (4) are under the ~8 test-example cutoff.
- *What I changed:* I checked the numbers against my notebook output before keeping them. I also questioned the "nothing changed" line and plan to try a tuning change (for example more epochs) instead of leaving the defaults. [Edit this if you decide differently.]

**Moment 2**

- *What I asked for:* What the model is supposed to learn, and whether I should tune anything.
- *What came back:* An explanation that it is a 3-class classifier (Positive / Negative / Neutral), and suggestions to try more epochs, a different learning rate or a smaller batch size, one at a time. It also pointed out that my training loss was still high and that the 29-post test set is too small to show small differences.
- *What I changed:* [Fill in what you actually did, e.g. "I tried 5 epochs and accuracy went from X to Y", or "I kept the defaults because ..."].

**Pre-labelling disclosure:**
1. I labelled the first 43 posts myself.
2. I worked out the labelling instructions from those.
3. I used AI to collect the rest of the posts.
4. I used AI to pre-label them, and I read and checked every one of them.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
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
