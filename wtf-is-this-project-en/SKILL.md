---
name: wtf-is-this-project-en
description: Turns an unfamiliar project (GitHub repo, web article, or local text file/directory) into a project brief that someone who has never written code can read in one pass. Use when the user wants to quickly understand what an open-source project does, how to get started, or whether it is worth using. Output is a plain-text chat message; it creates no files (no HTML, MD, or PDF). English output. Not for multimodal inputs such as video or audio.
agent_created: true
---

# wtf-is-this-project-en

`wtf-is-this-project-en` turns an unfamiliar source project into a **project brief**. It changes **understanding**, not translation — paraphrasing the README doesn't count.

The reader has never written code: "repository", "shell", and "dependency" need explaining; "variable" and "file" do not.

## Output form

**It goes straight into the chat. It is not a file.** The brief lives in the conversation between you and whoever asked — they scroll and read, they don't open an attachment. **This skill creates no `.html`, `.md`, `.pdf`, or any other file.** The source project may well be a repo or a markdown file; the output is always a chat message.

## Read these three first

Do not start writing until you've read them. They define what "good" means:

| File | What it governs |
|---|---|
| `references/style-rules.md` | Content and structure: the six-section skeleton, S/W/T/N rule groups |
| `references/ai-flavor-checklist.md` | Syntax: the English AI-flavor checklist, groups A/B/C/D |
| `references/golden-sample.md` | A human-approved full sample — match its density and tone |

Style rules govern content and structure; the AI-flavor checklist governs sentence wording. The two do not overlap.

## Formatting — GPT style

Write it the way ChatGPT formats answers. **Visual anchors + short sentences + numbering** let the reader scan in one pass.

### Four principles

(1) **Headings must use Markdown syntax**: `#` for the document's single top title, `##` for the six body sections. That's what makes the chat window render them at different sizes. **Do not fake a heading with `**bold**`** — bold is inline styling, it carries no heading level, and it renders a size smaller than a real heading.

(2) **Section anchors**: put one emoji in front of each heading's text — `🔥` `⚡` `📌` `🎯` `🛠` `🎨`. **The emoji is a prefix, not the heading itself**: write `## 🔥 How to install and use it`, not `## 🔥`, and not `**🔥 How to install and use it**`.

(3) **Short sentences + numbering**: number items `1. 2. 3.` rather than using Markdown list syntax (which adds unwanted indentation). Keep sentences short; break long ones up.

(4) **Visual density**: at most one bold, one inline-code span, and one emoji per sentence. More than that and it turns to noise.

### Element usage

| Element | Use for |
|---|---|
| `🔥` `⚡` `📌` `🎯` `🛠` | Section-opening anchors |
| `inline code` | File names, command names, config keys, error codes, URL path segments |
| `**bold**` | The keyword in a passage (no more than 2–3 per paragraph) |
| `→` | "means" / "is equivalent to" / flow direction |
| `❓` | Self-posed questions, leading into the next passage |
| `✅` `❌` `⚠️` | Status marks, contrasts |
| `➡️` `⬇️` | Between nodes in a flow |
| `🟦` `🟪` `🟩` `🟥` | Flow-chart node colors |
| `😂` `🤔` `😅` | Occasional tone emoji — no more than one per paragraph |

### Strictly forbidden

- Indentation (never use Tab or spaces to carry structure)
- **Faking a heading with `**bold**`** — it drops a size and loses the hierarchy
- **Using only an emoji as a heading** (e.g. `## 🔥` with no text) — emoji is a prefix, not the heading
- Mixing ASCII box-drawing (`┌─┐│└┘`) with colored emoji — different font metrics make this render crooked

### Tables, code blocks, charts: keep them as they are

- **Tables**: use Markdown tables for comparative content (When you'd reach for it, the self-check).
- **Code blocks**: for genuinely runnable commands, character diagrams, or real code snippets.
- **Charts**: plain text + emoji anchors + arrows. Never rely on Unicode box-drawing that only some fonts support.

### Template

A typical shape. **Note the headings are `#` / `##`, with emoji as prefix only**:

~~~
# 🔥 [Closest to "a project an idiot could understand"]

## 📌 Three candidates

1. `idiot-proof-github.skill` → "a GitHub project any fool can use and understand"
   Reads naturally — **idiot-proof** is a fixed expression in English.
2. `github-for-absolute-idiots.skill` → "GitHub for utter idiots"
   Beautifully over the top, **exactly the flavour you described**.
~~~

## Step 1: Probe the asker's environment

Before producing anything, work out the environment of whoever asked:

- **Operating system**: macOS / Windows / Linux. Detect from `uname -a`, environment variables, file paths, or just ask.
- **AI tools already in use**: Claude Code / Cursor / Codex / Copilot / Gemini CLI.
- **Package managers available**: brew / apt / dnf / scoop / winget / chocolatey.
- **Comfortable with a shell?**: if yes, give commands; if no, give download links plus a GUI walkthrough.

Where the environment is unknown, leave a placeholder — "**use your platform's default**". Never guess.

## Step 2: Ingest

The source project can be a GitHub repo, a web article, or a local file or directory. All three follow **the same output structure**, diverging only at "how to read it".

**Read only. Never clone.** Don't leave a third-party repo on the user's machine.

Spin up sub-agents by size:

(1) Under 20 source files: none, read directly
(2) 20–100: 3–4 sub-agents
(3) Over 100, or a monorepo: 6–8

**Cap at 8.** Beyond that, the cost of merging their output eats the concurrency gain.

**Speed is the first principle**, ranked above coverage. Read the trunk if you can't read it all; drop a section entirely if you can't write it — the skeleton tolerates missing sections, never padding.

**One important caveat**: nearly everything a beginner brief needs lives in the README, the project site, and the docs — **not in the source**. Sending eight sub-agents to read 127 `.rs` files is slower and mostly wasted. Source-file count is a poor proxy for "how much material there is to read."

## Step 3: Run the facts pass

This section has exactly one purpose: **check less**, not more.

(1) **Omit numbers that would need verifying.** Star counts, open issue counts, version numbers — each one costs a round trip to verify, or risks being copied wrong, and the reader can't decide anything with them. Don't ask, don't look, don't write them.
(2) **Check anything that goes in the body against its original source.** Don't copy what a sub-agent reports; use what the docs actually and stably state. If it isn't going in the brief, don't look it up.
(3) **Localized docs may be stale.** Translations usually lag the English original, and even command syntax can have changed. Prefer the English original.

## Step 4: Write

Six sections, order not negotiable. Omit a section entirely if there's nothing for it; never reorder.

1. **How to install and use it** (incl. prerequisites)
2. **What problem it solves**
3. **When you'd reach for it** (a comparison table)
4. **Core concepts**
5. **What you can do once it's installed** — write **effect signals**: how would the reader know it worked. Not a feature list
6. **Where its edges are**

Put one source line between the H1 and section 1: `Source: <url> · language · license`.

End with a Q&A block: **2–3 two-line Q&A pairs** plus an **unexpanded details list** (one line each, entry points only, not expanded).

**The old rule still holds inside section 1**: first sentence is `project name + verb` giving the definition, second sentence draws the boundary, then the install steps.

### "Install it" must give a direct download link ❗

**Don't write "go to the website", "see the site", "check the homepage".** To a beginner that says nothing.

(1) If the project has **GitHub Releases**: call the API, get the current version and the per-platform packages, and **paste the concrete download URL for the reader's OS into the brief**.
(2) If a platform package manager covers it (brew / winget / apt): write the command out, branched by the reader's OS.
(3) If it's source-build only: give the command for their OS, and **don't just throw `git clone && npm install` at them** — add a line like "if you're not comfortable with a terminal, ask someone who is to help you through it."

### "How to use it" matches the reader's environment

If the probe step told you which AI tool they use, write the steps for that tool. **Don't list every tool** — only the one they actually have.

Length is decided by content. No word-count floor or ceiling.

## Step 5: Self-check

Go through it line by line; fix anything that fails:

- [ ] Someone who has never written code can say what the project solves
- [ ] Every unfamiliar term is annotated, and the sentence still stands with the annotation removed
- [ ] No bare code in the body — only "one line + a command or function name" hooks
- [ ] Structural emoji used by role, **and the same emoji keeps the same role throughout**
- [ ] Headings use `#` / `##`, **not `**bold**`**; emoji is a prefix, not the heading
- [ ] Every major section opens with an emoji anchor (`🔥` `⚡` `📌`)
- [ ] Key terms in `inline code`; key judgments in `**bold**`
- [ ] Flow and contrast content uses a plain-text + emoji-anchor diagram; no Unicode box-drawing mixed with colored emoji
- [ ] The "install it" section gives a **direct download link or command**, not "go to the website"
- [ ] AI-flavor checklist: Group B hits 0
- [ ] Length set by content, no padding
- [ ] Within the time baseline (a human writing a brief of this quality takes about 14 minutes)
- [ ] Output is a plain chat message; no file was created
- [ ] No indentation anywhere — structure comes from the numbering

## What not to do

- No multimodal input (video, audio)
- No non-English output
- **No files created** — everything is a chat message
- No "you might also want to ask" interaction prompts
- Don't dig into implementation: pointing at where a key file lives is fine, explaining how it works internally is not
- Don't list engineering status: open issue counts, bug lists, version drift, doc contradictions — a beginner can't act on any of it
- **Don't look up unstable numbers**: stars, issues, version numbers
- Don't sugarcoat: correct numbers the reader would misread, and say plainly when not to use it
- **Don't pass the buck**: never write "go to the website" — give the direct link
