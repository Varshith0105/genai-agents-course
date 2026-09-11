# GenAI · Agentic AI · AI Agents — course repo

Instructor: **Ajit Byru** · `ajitbyru@gmail.com` · github.com/byruajit

This repository is the single source of truth for the course: every command shown in class is here, character for character. If a slide and this README disagree, the README wins.

**Rule for the whole course: every Python command starts with `uv run`.** Never plain `python`.

---

## Session 1 — set up your machine (Windows, PowerShell)

Already have VS Code, Git or Python? Keep them. Skip the matching install line and run the version check only. Everyone runs steps 1, 2 and 5–8.

| # | Step | Command |
|---|---|---|
| 1 | Install uv, then **close and reopen the terminal** (have uv? `uv self update`) | `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 \| iex"` then `uv self version` |
| 1b | Only if step 1 still says "not recognized" after reopening | `[Environment]::SetEnvironmentVariable('Path', $env:Path + ';' + $HOME + '\.local\bin', 'User')` → reopen |
| 2 | Python 3.12 via uv (do this even if you have Python; it never touches yours) | `uv python install 3.12` then `uv python list` |
| 3 | Git and VS Code, then reopen the terminal (already installed? verify only) | `winget install --id Git.Git -e` · `winget install --id Microsoft.VisualStudioCode -e` · `git --version` · `code --version` |
| 4 | Clone and open — never in `C:\WINDOWS\system32` | `cd ~\Documents` · `git clone https://github.com/byruajit/genai-agents-course.git` · `cd genai-agents-course` · `code .` |
| 5 | Install pinned packages (VS Code terminal, Ctrl+`) | `uv sync` |
| 6 | Private config — paste your **team** key as `API_KEY`; do not touch `MODEL`; no quotes; no trailing space | `copy .env.example .env` (Mac/Linux: `cp .env.example .env`) |
| 7 | First LLM call — read the token count | `uv run python hello.py` |
| 8 | **Checkpoint** | `uv run pytest tests/test_setup.py` → `3 passed` |
| 9 | Background / homework | ollama.com → install → `ollama pull llama3.2:3b` |

### Mac / Linux differences
Step 1: `curl -LsSf https://astral.sh/uv/install.sh | sh` · Step 3: `xcode-select --install` (Mac) or `sudo apt install git` (Ubuntu); VS Code from code.visualstudio.com, then Command Palette → "Shell Command: Install code command in PATH" · Step 6: `cp` not `copy`. Everything else is identical.

### Switching to Ollama (rate limits, or private data)
In `.env`, comment the three Groq lines and uncomment the three Ollama lines. No code changes.

---

## Troubleshooting — the three errors that cover almost everything

**`uv` is not recognized** — you did not reopen the terminal. Close every terminal (including VS Code's) and open again. Still failing → step 1b.

**401 invalid API key** — open `.env` (not `.env.example`). No quotes around the key, no trailing space, not the placeholder. If in doubt, ask the instructor for a fresh team key.

**Ollama: model not found / connection refused** — not found → `ollama pull llama3.2:3b`. Connection refused → Ollama is not running: check the tray icon, or run `ollama serve` in a second terminal.

Also seen: a warning that `UV_NATIVE_TLS` is deprecated — harmless, ignore. `uv version` (no dashes) errors outside a project — use `uv self version`.

---

## Keys
Team keys are shared by four people and have a spend cap. They live in `.env` and nowhere else. A key in chat, code or a screenshot is revoked and re-issued.

## Links
- Community channel: _(added by instructor)_
- Submission form: _(added by instructor)_
- Baseline quiz: _(added by instructor)_
- Fix videos: _(coming)_

## Layout
```
hello.py                    Session 1 first call
tests/test_setup.py         Session 1 checkpoint
cheatsheet/python-for-agents.md
.env.example                copy to .env
pyproject.toml              pinned dependencies (uv sync)
```
Modules are added as the course progresses (`module01/ … module14/`).
