# 🔥 rtk — Project Brief

Source: `github.com/rtk-ai/rtk` · Rust · Apache-2.0

## 🛠 How to install and use it

`rtk` sits between your AI coding tool and the shell, compressing command output before it reaches the AI. It changes the **output**, not the command — commands still run normally, the copy handed to the AI is just stripped of noise.

**Install it**, any one of these:

```
brew install rtk                    # macOS and Linux, simplest
curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh
cargo install --git https://github.com/rtk-ai/rtk
```

**Use it**, three steps:

1. `rtk init -g` → installs the hook into your AI tool. Add `--agent cursor` for Cursor, `--gemini` for Gemini CLI.
2. Restart your AI tool.
3. Work normally. You never type `rtk` again — commands are rewritten automatically.

**Before you install**:

(1) A supported AI coding tool. It works with Claude Code, Cursor, Codex, Copilot, Gemini CLI and others.
(2) Some filters shell out to a search tool called `ripgrep`. On Windows you may need to install it separately, or you'll see a "Binary 'rg' not found on PATH" warning.
(3) It only intercepts **shell commands**. Your AI tool's built-in file-reading and search features don't go through the shell, so it can't touch those.

## 💡 What problem it solves

Before your AI can change code, it has to see the current state — `git status` to see what changed, `cargo test` to see what broke. All of that output gets read into the **context window** (context window: the limit on how much the AI can hold at once; when it fills, earlier content gets dropped). And the AI measures text in **tokens** (token: the unit the AI uses for both capacity and billing). A `git status` is twenty lines; a failing test run is hundreds. A few rounds and the window is full.

`rtk` compresses those hundreds of lines down to a dozen before handing them over.

```
🟦 AI coding tool ──▶ 🟪 rtk proxy ──▶ 🟩 shell
   asks for work         rewrites +         git / ls /
                         compresses         cargo test
                              │
                              ▼  filtered output returned

❌ Without rtk:   AI ──▶ shell ──▶ ~2000 tokens raw ──▶ entire thing into the window
✅ With rtk:      AI ──▶ shell ──▶ [rtk trims] ──▶ ~200 tokens ──▶ into the window
                                        └─▶ on failure, full log saved separately
```

## 🎯 When you'd reach for it

| Your situation | Use it? |
|---|---|
| You use an AI coding tool that runs shell commands on its own | Yes |
| Your AI runs tests, checks git status, lists directories many times a day | Yes |
| You only occasionally ask the AI to write code and it never touches the shell | No |
| Your AI tool only uses its own built-in file and search features | No |

## 📌 Core concepts

1. `filter` → the compression rules written for one specific command, deciding which lines of its output stay and which get dropped.
   **Test**: it covers 100-plus commands. **A command with no matching filter passes through untouched and counts as 0% saved** — it compresses what it recognizes, not everything.

2. `hook` → the interception point your AI tool exposes before running a command. `rtk` hangs there and swaps `git status` for an equivalent compressed version.
   **Test**: after installing you never type `rtk` yourself. You work normally and the rewrite happens on its own. Removing it is one command.

3. `tee` → saving the command's complete raw output to disk separately. Compression only affects the copy the AI sees.
   **Test**: on by default for failures only. Not optional in spirit — compression is "drop what looks like noise," and when it drops the wrong thing you'd never know. The saved copy is how you get back to the original.

## ⚡ What you can do once it's installed

Four signals that it took effect:

(1) Run `git status` — the AI receives compressed output, not the raw twenty-plus lines
(2) Run `rtk gain` — it reports what it saved (this is **estimated as bytes ÷ 4**, not an exact token count; it ships no tokenizer)
(3) Run `rtk discover` — it lists command by command which ones get compressed and which pass through
(4) One command removes it — hook off, nothing left behind

## ⚠️ Where its edges are

It reduces **bash output bytes**, not your bill. Command output is only one contributor to input tokens, input tokens are only part of the bill, and the reduction dilutes at every step.

**When not to use it**: you only occasionally ask the AI for code and it never touches the shell — then it does nothing for you. It optimizes the act of "the AI running commands repeatedly." No such act, no optimization.

## ❓ You might also ask

1. **Do I have to type `rtk` myself?** No. The hook rewrites commands automatically; you work normally.

2. **Will it compress away something important?** It can — compression is lossy. That's why it saves the raw output separately when a command fails, so you can get back to the original.

3. **What happens to a command with no matching filter?** It passes through untouched. No compression, no error. It counts as 0% saved.

**Not expanded above** (ask if you want any of them):

(1) The config file at `~/.config/rtk/config.toml` — exclude specific commands, control when raw output is saved
(2) The full list of supported AI coding tools
(3) Per-command compression rates; `rtk gain --graph` plots the trend
(4) Where the raw logs for failed commands are stored
