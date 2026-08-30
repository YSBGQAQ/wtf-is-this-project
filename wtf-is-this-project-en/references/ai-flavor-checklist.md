# AI Flavor Checklist

Adapted from `humanizer` v2.2.0. Use it to check the **sentence-level** wording of a project brief before delivering it.

This checklist governs **syntax only**. Content and structure are governed by `style-rules.md`. The two do not overlap.

## Provenance and rulings

The source file divides into four rulings:

| Range | Content | Ruling |
|---|---|---|
| 1–437 | 24 executable patterns + "PERSONALITY AND SOUL" | Adopted (Groups A / B / C / D) |
| 438–476 | Chinese worked example | Not applicable to the English version |
| 477–535 | AI-detection reduction workflow (Turnitin, CNKI, etc.) | **Discarded** — unrelated to writing quality |

Note the symmetry with the Chinese version: ADR-0003 required *translating* these rules into Chinese because the English patterns don't survive the language switch. Here they apply natively — no translation needed. ADR-0002 (dropping the passage-level instructions) applies to both versions.

---

## Group A: Universal — holds in any language

These are rhetorical habits, not vocabulary. Keep them all.

### A1. Don't inflate significance
Don't append a statement about how important the thing is. State what it does.
- Bad: "The Statistical Institute of Catalonia was officially established in 1989, marking a pivotal moment in the evolution of regional statistics."
- Good: "The Statistical Institute of Catalonia was established in 1989 to collect and publish regional statistics independently from Spain's national office."

### A2. No formulaic "Challenges and Future Prospects" sections
- Bad: "Despite its industrial prosperity, Korattur faces several challenges... Despite these challenges, it continues to thrive."
- Good: "Traffic congestion increased after 2015 when three new IT parks opened."

### A3. Use "is/are" — don't avoid the copula
- Bad: "Gallery 825 serves as LAAA's exhibition space. The gallery features four rooms and boasts over 3,000 square feet."
- Good: "Gallery 825 is LAAA's exhibition space. It has four rooms totaling 3,000 square feet."

### A4. Skip negative parallelisms
"Not only...but also" / "It's not just X, it's Y" — fine once, AI-sounding when repeated.
- Bad: "It's not just about the beat; it's part of the aggression. It's not merely a song, it's a statement."
- Good: "The heavy beat adds to the aggressive tone."

### A5. Don't pad to groups of three
- Bad: "The event features keynote sessions, panel discussions, and networking opportunities. Attendees can expect innovation, inspiration, and industry insights."
- Good: "The event includes talks and panels, with time for informal networking between sessions."

### A6. Don't cycle synonyms
Pick one word for a concept and keep it. Swapping names to avoid repetition reads as machine-generated.
- Bad: "The protagonist faces many challenges. The main character must overcome obstacles. The central figure eventually triumphs."
- Good: "The protagonist faces many challenges but eventually triumphs."

### A7. No false ranges
"From X to Y" only works when X and Y sit on the same scale.
- Bad: "From the singularity of the Big Bang to the grand cosmic web, from the birth of stars to the dance of dark matter."
- Good: "The book covers the Big Bang, star formation, and current theories about dark matter."

---

## Group B: English-specific — the original patterns

These carry explicit **words to watch**. Run them against the draft literally.

| # | Pattern | Words to watch |
|---|---|---|
| B1 | Inflated significance | stands/serves as, is a testament to, a vital/crucial/pivotal role, underscores its importance, reflects broader, symbolizing, setting the stage for, marks a shift, key turning point, evolving landscape, indelible mark, deeply rooted |
| B2 | Inflated notability | independent coverage, local/regional/national media outlets, written by a leading expert, active social media presence |
| B3 | Superficial `-ing` analysis | highlighting, underscoring, emphasizing, ensuring, reflecting, symbolizing, contributing to, cultivating, fostering, encompassing, showcasing |
| B4 | Promotional language | boasts a, vibrant, rich (figurative), profound, enhancing its, exemplifies, commitment to, natural beauty, nestled, in the heart of, groundbreaking (figurative), renowned, breathtaking, must-visit, stunning |
| B5 | Vague attribution | Industry reports, Observers have cited, Experts argue, Some critics argue, several sources (when few are cited) |
| B6 | Overused AI vocabulary | Additionally, align with, crucial, delve, emphasizing, enduring, enhance, fostering, garner, highlight (verb), interplay, intricate/intricacies, key (adjective), landscape (abstract noun), pivotal, showcase, tapestry, testament, underscore (verb), valuable, vibrant |
| B7 | Copula avoidance | serves as, stands as, marks, represents, boasts, features, offers |
| B8 | Knowledge-cutoff disclaimers | as of [date], up to my last training update, while specific details are limited, based on available information |
| B9 | Collaborative artifacts | I hope this helps, Of course!, Certainly!, You're absolutely right!, here is a..., let me know |
| B10 | Sycophantic tone | Great question!, You're absolutely right, That's an excellent point |
| B11 | Filler phrases | in order to → to; due to the fact that → because; at this point in time → now; in the event that → if; has the ability to → can; it is important to note that → (delete) |
| B12 | Excessive hedging | could potentially possibly, might have some effect, it may be argued |
| B13 | Generic positive conclusions | The future looks bright, exciting times lie ahead, a major step in the right direction |
| B14 | Title Case in headings | Use sentence case: `## Strategic negotiations and global partnerships` |
| B15 | Curly quotation marks | Use straight quotes `"..."` in English output |

Worked example (from the source):

> Before: "The new software update serves as a testament to the company's commitment to innovation. Moreover, it provides a seamless, intuitive, and powerful user experience—ensuring that users can accomplish their goals efficiently. It's not just an update, it's a revolution. Industry experts believe this will have a lasting impact."
> After: "The software update adds batch processing, keyboard shortcuts, and offline mode. Early feedback from beta testers has been positive, with most reporting faster task completion."

---

## Group C: Forbidden — conflicts with this project

These come from the platform-rewrite prompts in the source. They target **AI-detection scores**, not readability. Using them would destroy the "lean and clean" goal.

| Instruction | Why forbidden |
|---|---|
| "Shuffle the logical order; don't follow problem → analysis → solution" | Directly opposes "lean and clean." A beginner reader needs a clear order, not jumps. |
| "Add transitional thinking between points; increase length by ~30%" | Padding is not de-AI-ing. Our length is set by content, nothing else. |
| "Insert 5 expressions of uncertainty" | Manufactured hedging is B12. Honest "I couldn't figure this out" is different — that we keep. |
| "Pretend you're a student writing at 3 a.m.; rambling and repetition are fine" | Opposes concision. Varied sentence length is fine; rambling is not. |
| "Fragment the text across several places to mimic human thought jumps" | Opposes "readable in one pass." |

**Kept** (they align with our goal): the instruction to strip "firstly / in conclusion / it is worth noting"; the one about mixing long and short sentences; the one about adding 2–3 concrete data points or examples; the one about showing the author's reasoning process.

---

## Group D: Overridden by project rules

The source opposes these. This project needs them, so the project rule wins.

### D1. Boldface
The source says minimize. **We allow structural bold** — term names, key judgments. Forbidden: bolding whole paragraphs, or bold in every sentence.
Test: if you remove the bold, can the reader still scan and find the key points?

### D2. Inline-header vertical lists (`- **Point:** explanation`)
The source says convert to prose. **We allow them in the detail list** at the end of a brief. Use sparingly in body prose.

### D3. Emoji
The source says delete all. **We use them structurally** — see `style-rules.md`. Pure decoration is still forbidden.

---

## Add soul

Removing AI patterns is only half the job. Sterile, voiceless writing is just as obviously machine-made.

Signs of soulless writing (even when technically clean):
- Every sentence the same length and shape
- No opinions, just neutral reporting
- No acknowledgment of uncertainty or mixed feelings
- No first person where it fits
- No humor, no edge, no personality

How to add it:
1. **Have opinions.** React, don't just report. "I'm genuinely not sure how to feel about this" beats a neutral list of pros and cons.
2. **Vary your rhythm.** Short punchy sentences. Then longer ones that take their time. Mix them.
3. **Acknowledge complexity.** "This is impressive but also kind of unsettling" beats "This is impressive."
4. **Use "I" when it fits.** "Here's what gets me..." signals a real person thinking.
5. **Let some mess in.** Perfect structure reads as algorithmic. Asides and half-formed thoughts are human.
6. **Be specific about feelings.** Not "this is concerning" but "there's something unsettling about agents churning away at 3 a.m. while nobody's watching."

---

## How to use

Run the draft against Groups A → B → C → D. Report hits:

```
Hits: B6 (AI vocabulary) x 2
  - "Additionally, it is worth noting that the tool is fast" -> delete both
  - "The tool represents a key shift in workflow" -> "The tool changes the workflow"
Hits: A5 (rule of three) x 1
  - "faster, cheaper, and more accurate" -> "faster and cheaper"
Group B: 0 remaining
Group C: confirmed not used
```

**Bar: Group B must hit 0.** Group A should hit 0; keep any exception only with a stated reason.
