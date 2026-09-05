# Documentation project instructions

## About this project

- This is the FairStandard docs site, built on [Mintlify](https://mintlify.com) and served at developers.fairstandard.com.
- Pages are MDX files with YAML frontmatter. Configuration lives in `docs.json`.
- Two tabs. **Platform Overview** is written by people. **API Documentation** is generated per service. Read `README.md` before editing anything.
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP, and the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, for Mintlify questions.

## Do not edit generated pages

Everything under `services/` and `openapi/`, and the service groups in the `API Documentation` tab of `docs.json`, is regenerated three times a day from the service repos by `~/.claude/docs-site-build/run.sh`. Edits there are overwritten. Fix the source file in the service repo (`README.md`, `CONTEXT.md`, `docs/adr/*.md`, or the FastAPI app) instead.

Hand-written: every Platform Overview page, `how-this-site-is-built.mdx`, and the rest of `docs.json`.

## Names

- The company is **FairStandard**. The application is **Vero**. Say Vero when you mean the app and FairStandard when you mean the company. The wordmark reads "Vero by FairStandard".
- Use "service" for one of the 21 repos, "docs site" for this site, and "the build" for the scheduled regeneration.
- Use the domain words from each service's `CONTEXT.md` (its Domain model page) and avoid the words it lists under _Avoid_.
- Product nouns the platform owns take Title Case: Case, Deadline, Record, Finding, Phase, Records Index. Everything else is sentence case.

## Voice

The voice is the Vero design system's (`~/.claude/skills/fairstandard-design/readme.md`, "Content fundamentals"). In short:

- **Two registers.** Platform Overview pages are Guided: second person, plain language, the same facts, no advice. API Documentation pages are Professional: third person, court and service vocabulary, codes and identifiers shown.
- Talk like a competent colleague, not like software. Numbers live inside sentences.
- Every ranking or recommendation states its reason.
- Dates are absolute and relative together ("Aug 14, 2026 · 10 days out"). Never a raw timestamp in prose.
- The court's words are quoted, not paraphrased. A Guided page gives the plain label and still shows the code.
- Limits are stated as facts, with the reason. Empty states reassure; never celebratory.
- Never emoji, exclamation marks, "oops", marketing verbs, or anything that reads as legal advice. A public page that touches legal process carries "Vero explains legal process. It does not give legal advice."
- Em dash for the aside, middot for the metadata join, curly quotes for anything a human said.
- One idea per sentence. High-school reading level. Bold for UI elements, code formatting for file names, commands, paths, and code.

## Content boundaries

- Do not document `platform`; it is out of scope for this site.
- Do not paste secrets, tokens, or internal hostnames into pages.
- Run `mint validate` and `mint broken-links` (with Node 22 on PATH) before finishing any change.
