<p align="center">
  <img src="./assets/readme/hero.svg" width="100%"
       alt="wtf-is-this-project: turn any project into a brief that someone who has never written a line of code can read in one sitting">
</p>

<p align="center">
  Two agent skills that turn any project into a beginner-readable brief.
</p>

<p align="center">
  <a href="./README.md">中文</a> · <strong>English</strong>
</p>

## What problem it solves

You throw a GitHub project at it and want to know what it's actually for. The README usually doesn't help — it speaks to people who already know the field: terms without explanations, install commands and config snippets packed in tight, and after reading it you still don't know whether you should use it.

This skill doesn't restate the README. It **re-explains**: splits the project into six sections and rewrites it in plain words someone who has never written a line of code can follow. Output goes straight into the conversation. No files created.

## Real output

Excerpt of what running on `rtk` produces:

> ## 🛠 How to install and use it
>
> `rtk` sits between your AI coding tool and the shell, compressing command output before it reaches the AI. It changes the **output**, not the command — commands still run normally, the copy handed to the AI is just stripped of noise.
>
> **Install it**, any one of these:
>
> ```
> brew install rtk                    # macOS and Linux, simplest
> curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh
> cargo install --git https://github.com/rtk-ai/rtk
> ```
>
> **Use it**, three steps: `rtk init -g` to install the hook ➡️ restart your AI tool ➡️ work normally; commands get rewritten automatically.

Full samples: [English](./wtf-is-this-project-en/references/golden-sample.md) · [中文](./wtf-is-this-project-cn/references/标杆样本.md)

## Why not "just ask AI to summarize"

Two layers of rules, each does one job, no overlap:

| Layer | Who owns it | Contents |
|---|---|---|
| Content & structure | `style-rules.md` | Six-section skeleton + S/W/T/N four-rule set, distilled from 25 Matt Pocock articles |
| Sentence wording | `ai-flavor-checklist.md` | AI-flavor A/B/C/D checklist, from humanizer's English originals |

The split is hard: the wording checklist only governs sentence-level phrasing; style rules only govern content and structure. So output won't be "reads smoothly but loosely structured", nor "neat structure but full of AI-speak".

## The six-section skeleton

<p align="center">
  <img src="./assets/readme/skeleton.svg" width="100%"
       alt="The six-section skeleton: install and use, what problem it solves, when to reach for it, core concepts, effect signals, where its edges are">
</p>

Order is fixed. Missing content → drop the whole section. **Missing sections allowed. Reordering or padding is not.**

Two deliberate design choices:

- **Install & use comes first.** The pure beginner's only action item lives in this section; it deserves the space.
- **Section 5 documents effect signals, not a feature list.** It answers "how does the reader know it's working?".

## How to use

| Version | Directory | name | Output |
|---|---|---|---|
| Chinese | `wtf-is-this-project-cn/` | `wtf-is-this-project` | Chinese |
| English | `wtf-is-this-project-en/` | `wtf-is-this-project-en` | English |

Copy the whole directory into your skills folder:

```bash
# User-level: works for every project
cp -r wtf-is-this-project-en ~/.workbuddy/skills/

# Or project-level: only this repo
cp -r wtf-is-this-project-en .workbuddy/skills/
```

Then drop a project at it in conversation:

> Test this project: https://github.com/RoseKhlifa/Image-Studio

It first detects your OS, then gives a **direct download link** for that platform — never "go download it from the website".

## Repo layout

```
.
├── wtf-is-this-project-cn/        Chinese skill
│   ├── SKILL.md
│   └── references/                style-rules · ai-flavor-checklist · golden-sample
├── wtf-is-this-project-en/        English skill
│   ├── SKILL.md
│   └── references/                style-rules · ai-flavor-checklist · golden-sample
├── assets/readme/                 diagrams used by this page
├── docs/adr/                      architecture decision records 0001–0005
├── .scratch/wtf-is-this-project/  spec + tickets (local issue tracker)
├── CONTEXT.md                     domain model: glossary
└── AGENTS.md                      engineering config
```

## The two versions are not translations of each other

The English version has **two reference docs that sit closer to the source than the Chinese version does**:

- `style-rules.md` quotes 25 articles in their **original English** — the Chinese version is a translation, and drifts.
- `ai-flavor-checklist.md` uses humanizer's **English original patterns** — ADR-0003's "localize to Chinese" doesn't apply here; ADR-0002's deletions apply to both versions.

## Design decisions

Five deviations are recorded in `docs/adr/`:

| ADR | Decision |
|---|---|
| 0001 | ~~Dual delivery modes~~ **Deprecated**: HTML mode dropped, conversation-output only |
| 0002 | humanizer: keep only the sentence-syntax layer; drop the reorder/word-count-bloat instructions |
| 0003 | humanizer's English patterns must be localized for Chinese output |
| 0004 | Subagent concurrency capped at 8 |
| 0005 | Common Questions section deleted, then reinstated as **2–3 compressed entries** |

## Known edges

- **Not multimodal.** Video and audio are out of scope.
- **Doesn't verify drift-prone numbers.** Stars, issue counts, version numbers are never asked, fetched, or written — verifying them costs time, and drifting numbers don't help the reader.
- **Doesn't write engineering status.** Bug lists, doc contradictions, community debates — pure beginners can't act on them.
- **Leaves blank where it can't get info, with a note.** The cost is slower intake.

## License

MIT
