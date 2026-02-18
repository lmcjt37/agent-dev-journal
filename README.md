# Agent Dev Journal Skill

A journaling skill for AI coding agents that **captures decisions** and **stores conversation transcripts** directly inside your project—so you can remember *why* things were built a certain way, not just *what* changed.

It maintains three things at the **closest git repo root**:

- `Journal.md` — a curated, human-friendly learning journal (medium-fun, memorable, ~400–500 words per entry)
- `journal/decisions.md` — a searchable decision ledger (DR-### entries)
- `journal/transcripts/…` — full conversation transcripts (with **large tool outputs compressed to highlights**)

---

## Who this is for

- Developers using AI agents and wanting a reliable “paper trail” of **decisions + rationale**
- Teams who keep rediscovering the same pitfalls and want the lessons captured once
- Anyone who wants the benefits of ADRs + dev diaries without turning their repo into a paperwork museum

---

## What it does

### ✅ Decision tracking
The skill creates Decision Records when it detects:
- **Commitment language** (“we’ll do X because…”, “let’s go with Y…”), or
- A change that’s **expensive to revert** (architecture, data model, CI approach, etc.)

Each DR includes:
- context, decision, why, alternatives, tradeoffs, consequences, and links (PR/commit/issues when available)

### ✅ Transcript capture (with sanity)
It stores the **full conversation**, but if tool output is huge (logs, diffs, etc.), it saves:
- what ran / what changed
- 5–15 key lines
- outcome + next step

### ✅ A readable Journal.md
It appends a curated entry under “The Journey”:
- what happened, gotchas, fix, lessons learned
- analogies encouraged, humor *medium* (with occasional spice)

---

## How to use this skill

Install the skill Using skills.sh:

```bash
npx skills add https://github.com/lmcjt37/agent-dev-journal --skill agent-dev-journal
```

---

## What gets written to your repo

After a checkpoint, you should see:
- Journal.md
- journal/decisions.md
- journal/transcripts/YYYY-MM-DD__<branch>__<agent>.md

Naming rules:
- Repo root: closest git root via git rev-parse --show-toplevel
- Branch: git rev-parse --abbrev-ref HEAD (slashes sanitized to -)
- Agent name: detected if possible, otherwise [AGENT]
- Session boundary: branch + day (so you can span multiple days safely)


Prompts that work well
- journal checkpoint
- journal log this decision and include alternatives
- capture today’s transcript and extract DRs
- we just made an architecture decision—record it
- summarize what changed and why we did it, then checkpoint


## Redaction rules (what’s protected)

Automatically redacted (with notes):
- API keys / tokens / secrets (e.g., *_TOKEN, *_KEY, *_SECRET)
- Password-like fields
- Private key blocks (BEGIN PRIVATE KEY)
- Authorization headers (Authorization: Bearer …)
- Session cookies

If you want to expand redaction later (emails, internal hosts, customer names), add it to references/guidelines.md.

## FAQ

*Why not put everything in Journal.md?*

Because Journal.md is for humans. Transcripts and DRs are for future archaeology.
This skill keeps the narrative fun and the evidence searchable.

*Can it work across multiple projects?*

Yes. It always writes to the closest git root, so it naturally scopes to the current project.

*What if the repo doesn’t have Journal.md yet?*

The skill creates it automatically using the required outline and style guidelines.

---

## License

See [LICENSE.md](./LICENSE.md).

⸻

## Contributing

PRs welcome:

- Better redaction patterns
- Tighter decision detection
- Improved transcript compression heuristics
- Better “journal entry” narrative templates