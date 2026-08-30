# Style Rules

Induced from 25 articles of Matt Pocock's skills series on aihero.dev. Governs the **content and structure** of a project brief.

Sentence-level wording is governed by `ai-flavor-checklist.md`. The two do not overlap.

## Method

- Source: 25 URLs. **All 25 fetched successfully.**
- Five sub-agents each close-read five articles. The skim pass was done by **cross-group comparison**: a pattern reported by one group only counts as a rule if the other four groups corroborate it. Otherwise it's demoted to a one-off and recorded as such.
- Inductive, not deductive. The sub-agents were told to observe how the articles are actually written. They were given no framework to look for.

---

## 1. Structure

### 1.1 The skeleton: no exceptions across 25 articles

H1 plus H2 only — **not one H3 in the entire series**.

Between the H1 and the first H2 there is an **untitled preamble block** in three parts:

```
Install this skill            One shell command
Then type `/X` in your        How to invoke it
coding agent.
───
Source                       Repository link
```

Then the body, seven sections in the same order every time:

```
What it does
When to reach for it
Prerequisites                ← only about half the articles
〔1–3 article-specific sections〕
Common questions
It's working if
Where it fits
```

Fixed traits per section:

| Section | Hard traits |
|---|---|
| What it does | First sentence is the backticked skill name plus a verb. Straight to the definition, zero preamble. |
| When to reach for it | Opens with a verbatim template: `You invoke this by typing \`/X\`; the agent won't reach for it on its own.` |
| It's working if | **Every line is an observable behaviour**, not a principle. `It starts writing rather than asking you a fresh round of questions.` / `No code changed during the run.` |
| Common questions | Bold question in the reader's voice, then the answer. 3–9 pairs. |
| Where it fits | Closing routing note, last line usually points to `ask-matt`. |

### 1.2 The second paragraph sets the boundary

The most stable pattern in the series. Paragraph one defines; **paragraph two immediately says what it is not**:

> `codebase-design`: "It is a reference, not a process. There is no loop to run, no artifact it produces, no checkpoint where it asks you a question."
> `diagnosing-bugs`: "It never changes the code."
> `to-questionnaire`: "It grills you about the **send**, never the subject."
> `prototype`: "Throwaway is a constraint on how the code is *written*, not a promise to destroy it."

**Define, then immediately draw the boundary. It beats three more paragraphs of explanation.**

### 1.3 The project brief skeleton

Our reader is not an engineer, so section names move from the technical frame to the reader's frame.

Final shape: **six sections plus one closing Q&A block**.

| # | Section | Maps to |
|---|---|---|
| 1 | **How to install and use it** (incl. prerequisites) | Preamble (Install + Then type) + Prerequisites |
| 2 | **What problem it solves** | What it does |
| 3 | **When you'd reach for it** | When to reach for it |
| 4 | **Core concepts** | Article-specific sections |
| 5 | **What you can do once it's installed** | It's working if |
| 6 | **Where its edges are** | Where it fits |
| — | **You might also ask** | Common questions + unexpanded details |

**Two deliberate reorderings, one principle behind both: put what a beginner cares about first, push the optional to the end.**

1. **Install/use promoted to the top, absorbing `Prerequisites`.** He keeps Install / Then type in an untitled block above the body, one line each. We promote it to a real first section and expand it — it's the only part a beginner actually has to act on, so it earns the space. `Prerequisites` folds in because "what you need before installing" is the same thought; a separate section would break the flow of getting started.
2. **Q&A merged and pushed to the end.** `Common questions` compresses from 3–9 long pairs to 2–3 pairs of two lines each, then absorbs the unexpanded-details list. Both are "might want to know, doesn't need to be here now" — splitting them interrupts the read twice, so they sit together at the bottom.

**The old rule still holds inside section 1**: first sentence is `project name + verb` giving the definition, second sentence draws the boundary, and only then do you get to the install steps. Ten seconds to know what you're installing, then how.

**One nuance to calibrate**: section 5 maps to `It's working if`, which is about **signals that it took effect** — "how would the reader know it worked?" — not a feature list.

---

## 2. Style rules (S / W / T / N)

### S: Structure

- **S1** The first sentence of section 1 must be `project name + verb` giving the definition; the second sentence immediately draws the boundary; then the install steps. No "In this article…", no "Have you ever…".
- **S2** The second sentence of section 1 sets the boundary: what it does not do. Use the "X, not Y" shape.
- **S3** Two heading levels only. No third-level headings — core concepts use bold terms, not subheadings.
- **S4** Fixed six sections plus the closing Q&A block, order not negotiable. Omit a section entirely if there's nothing for it; never reorder.
- **S5** Section 5 writes **effect signals**: how would the reader know it worked. Not a feature list.
- **S6** No summary, no recap, no call to action. The last body section is "Where its edges are", not a review.

### W: Writing

- **W1** Second person `you` for the reader, third person `it` for the project. The author never appears as "I" — first person only shows up inside quoted reader remarks.
- **W2** Declarative by default. Imperatives appear when giving instructions, short and direct.
- **W3** Two sentence lengths: 3–8 word sentences standing alone to land an assertion; long sentences carrying definition and qualification. Never all mid-length.
  > `No.` / `Yes, and plenty of people did before it existed:` / `That is the whole skill.`
- **W4** **"X, not Y" is the signature move** — use it in every concept definition. Highest-density pattern in the series.
  > `shorter and clearer, not shorter and blunter` / `A quiz is a gate, not a formality` / `an index, not a store`
- **W5** "There is no X" shuts down things that don't exist, cleanly: `There is no alias.` / `There is no fix shipped yet.`
- **W6** Answer first, expand second — one sentence up front: `Not as a step of its own.` / `No, and a cap is deliberately out of scope.`
- **W7** Close paragraphs with a short judgment: `Nothing needs to exist before you start.`

### T: Terminology

- **T1** Four-part package: **name → definition → executable test → words to avoid**. His glossary entries have exactly this shape:
  > `Interface` — "Everything a caller must know to use it correctly: the type signature, plus invariants, ordering constraints, error modes" — _Avoid_: API, signature
- **T2** **Give a test, not an adjective.** The test has to be runnable on the spot:
  > `deletion test`: "Imagine deleting the module. If complexity vanishes, it was a pass-through."
  > "One adapter means a hypothetical seam. Two adapters means a real one."
- **T3** Restate in plain words right after naming; use a metaphor when the concept is abstract.
  > "an interface nearly as complex as the thing it hides" (explaining shallow)
  > "An agent that hears 'be brief' writes telegrams."
- **T4** Variant: set the scene first, land the term after.
  > "'One long form or three pages?' and 'how should this interaction feel?' are **ungrillable**: they need something to react to."
- **T5** A term annotation must leave the sentence self-sufficient **when the annotation is removed**. His version links terms out to a dictionary and the sentence still reads without the link; ours is a parenthesis that can be deleted without breaking the sentence.

### N: What not to write

- **N1** No opening preamble, no background, no "why this is needed."
- **N2** No summary section, no key takeaways, no call to action. The final section is "Where its edges are", not a recap.
- **N3** No marketing adjectives. The series never uses powerful / seamless / effortless.
- **N4** **Correct misconceptions, but don't list engineering status.** A narrowing of his approach — his readers are engineers, ours are not.

  | Write | Don't write |
  |---|---|
  | A number the reader will misread (the "90%" is bash output bytes, not your bill) | Open issue count, bug lists |
  | Scope limits (it only compresses commands it recognizes) | Version drift, stale install docs |
  | How it fails silently (compression silently not applied, no error) | Document contradictions, community disputes |

  Test: **can the reader make a decision from it?** If yes, write it. If it only tells them "this project is messy," skip it.
  Keep the correction to one sentence. Don't quote the English original, don't adjudicate which document is right.
- **N5** **Talk them out of it when it doesn't fit**, and qualify yourself directly with words like "honest":
  > "On a one-day build, skip it."
  > "the honest answer is that you don't need this."
  > "the honest map is that you'll use it less often than the other four options"
  > The routing table's last row reads `Nothing here fits well`
- **N6** No pleasantries, no disclaimers, no reassuring the reader.

---

## 3. Length

Measured across the 25 English articles: **about 600 to 2,300 words**, most landing between 1,100 and 1,900. Shortest are `wait-what` (~600) and `resolving-merge-conflicts` (~600); longest are `teach`, `code-review`, `prototype` (1,900–2,300).

**This is not a number to copy.** His readers are engineers; ours are not. Per-concept explanation costs more, overall depth costs less. Take the short end, and let content decide — no hard target.

---

## 4. Counterexamples

Recorded so one-offs don't get mistaken for rules:

| Article | Deviation |
|---|---|
| `wait-what` | Deviates most: no `Common questions`, no comparison table, no defect disclosure, about a third the length of `teach`. Almost pure mechanism. |
| `resolving-merge-conflicts` | Shortest tier, one body section, much weaker defect disclosure than the rest. |
| `writing-for-agents` | No tables at all — the only article in the series without one. |
| `grill-me` | Only article with `Common questions` placed **after** `It's working if`. |
| `setup-matt-pocock-skills` | Only one quoting reader remarks verbatim ("hard locked to github", "Config is death.") and the only one arguing against its own existence in `Common questions`. |
| `to-spec` | Fewest tables (one). |
| `tdd` | Adds a footer tagline; no other article does. |

**Strength tiers**:

- **No exceptions across 25**: the seven-section skeleton, H2-only, the second-paragraph boundary, second-person narration, author never appearing as "I", `It's working if` as observable behaviours.
- **About 4 in 5**: defect disclosure attributed to readers; `Where it fits` closing with a route to `ask-matt`; `When to reach for it` carrying a comparison table.
- **About 3 in 5**: `Prerequisites` present; subtitle and byline present.
