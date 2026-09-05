# Documentation project instructions

## About this project

- This is the FairStandard docs site, built on [Mintlify](https://mintlify.com) and served at developers.fairstandard.com.
- Pages are MDX files with YAML frontmatter. Configuration lives in `docs.json`.
- Two tabs. **Platform Overview** is written by people. **API Documentation** is generated per service. Read `README.md` before editing anything.
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP, and the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, for Mintlify questions.

## Do not edit generated pages

Everything under `services/` and `openapi/`, and the service groups in the `API Documentation` tab of `docs.json`, is regenerated three times a day from the service repos by `~/.claude/docs-site-build/run.sh`. Edits there are overwritten. Fix the source file in the service repo (`README.md`, `CONTEXT.md`, `docs/adr/*.md`, or the FastAPI app) instead.

Hand-written: every Platform Overview page, `how-this-site-is-built.mdx`, and the rest of `docs.json`.

## Terminology

- Use "service" for one of the 21 repos, "docs site" for this site, and "the build" for the scheduled regeneration.
- Use the domain words from each service's `CONTEXT.md` (its Domain model page) and avoid the words it lists under _Avoid_.

## Style preferences

- Active voice, second person ("you"), sentence case for headings.
- One idea per sentence. High-school reading level. No marketing words.
- Bold for UI elements, code formatting for file names, commands, paths, and code.
- No emoji, no decorative formatting.

## Content boundaries

- Do not document `platform`; it is out of scope for this site.
- Do not paste secrets, tokens, or internal hostnames into pages.
- Run `mint validate` and `mint broken-links` (with Node 22 on PATH) before finishing any change.
