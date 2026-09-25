# ContextForge — examples

**Turn any repository into an AI-ready context pack.**

`AGENTS.md` · `.cursorrules` · `CLAUDE.md` · `.github/copilot-instructions.md` · `GEMINI.md`

🔗 **Product: https://contextforge.lxsaihub.com**

This repo is the **example gallery**, not the product source. Every file in `examples/` was produced
by the live product from the input in `examples/example-input-tree.txt` — so you can judge the output
before paying for anything.

## The problem

Every team adopting Cursor, Claude Code, Codex or Copilot hits the same wall: the agent hallucinates
your conventions because they were never written down. The fix is a file. But hand-writing one costs
30–90 minutes per repo, and it rots the moment the stack changes.

ContextForge reads the tree you already have and drafts the file.

## How it works — two stages, and why that matters

| Stage | What happens | Depends on a model? | If the model is unavailable |
|---|---|---|---|
| 1 | **Deterministic extraction** — package manager, framework, test runner, CI, entry points, build/test/lint commands | **No** | Nothing changes. All facts still produced. |
| 2 | **Model-assisted prose** — turns those facts into readable conventions | Yes | 503 / 502 / 429, or a labelled rule-based draft |

Most tools in this space are a prompt wrapped in a form: model down, product dead, or worse — a
plausible lie. ContextForge puts the extraction in a layer that cannot fail, so the product degrades
instead of inventing.

Every fact is tagged:

- **`detected`** — read from a file you actually pasted (e.g. `scripts.build` in `package.json`)
- **`inferred`** — guessed from filenames, and *labelled as a guess* in the output

Anything it cannot determine at all goes into an **Open questions** section rather than being made up.

## What's in `examples/`

Generated from one input (a Next.js + Prisma + Vitest app):

| File | Agent that reads it |
|---|---|
| `AGENTS.md` | OpenAI Codex / generic agent harnesses |
| `.cursorrules` | Cursor |
| `CLAUDE.md` | Claude Code |
| `.github__copilot-instructions.md` | GitHub Copilot (real path: `.github/copilot-instructions.md`) |
| `GEMINI.md` | Gemini CLI / Code Assist |

Each carries a `source:` marker and a `RULESET_VERSION` stamp in its header. These five came through
the **rule-based path** — deterministic, so the same input always yields byte-identical output. The
model-assisted path writes the same sections in prose.

Read one and note what it does *not* do: it does not claim your tests pass, it does not invent a
command you never configured, and it tells you exactly what it could not work out.

## Why you should still read the output

A context file that confidently states a convention your repo does not follow is **worse than no
context file** — the agent trusts the instruction over the code. Treat every generated file as a
first draft: skim it, correct anything marked `(inferred)`, fill in the open questions, commit.

## Honest limits

- No repo connector, no OAuth, no GitHub App. You paste a tree; nothing is stored.
- Rule-based output is factual but terse. The model-assisted pass is what makes it readable.
- The fair-use quota is per-instance (serverless memory), not a global hard limit. A global limit
  needs KV/Edge Config and is not shipped.
- It cannot guarantee an agent stops hallucinating. Nothing can. It gives the agent better evidence.

## Links

- **Product:** https://contextforge.lxsaihub.com
- **Fleet hub (139 tools):** https://lxsaihub.com
- **Contact:** lixingliangsy@163.com

## License

MIT — see [LICENSE](LICENSE).
