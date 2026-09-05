# FairStandard docs

The FairStandard docs site, hosted on Mintlify at developers.fairstandard.com. Login required.

Two tabs: **Platform Overview** (the product guide, written by people) and **API Documentation** (one group per service, generated from the service repos three times a day).

## What is in here

| Path | What it is | Who writes it |
| --- | --- | --- |
| `introduction.mdx`, `concepts/`, `case-management/`, `learning-center/`, `marketplace/`, `attorneys/`, … | Platform Overview tab | People |
| `<section>/litigants/*.mdx`, `<section>/attorneys/*.mdx` | Platform Overview tab, one folder per reader per surface | People, to `anatomy.json` |
| `<section>/developers/*.mdx` | Developer guides in the API Documentation tab | People, to `anatomy.json` |
| `anatomy.json` | The sections, audiences, page kinds, and rules the hand-written pages follow | People |
| `how-this-site-is-built.mdx` | About page in the API Documentation tab | People |
| `services/<repo>/index.mdx` | The repo's `README.md` | The build |
| `services/<repo>/domain-model.mdx` | The repo's `CONTEXT.md` | The build |
| `services/<repo>/decisions/*.mdx` | The repo's `docs/adr/*.md` | The build |
| `openapi/<repo>.json` | The OpenAPI document the running app produces | The build |
| `docs.json` | Site config. The service groups in the API Documentation tab are regenerated; the rest is hand-kept | Both |

Everything under `services/` and `openapi/` is overwritten three times a day. To change one of those pages, change the source file in the service repo.

## How the build works

A launchd job on the FairStandard build machine (`com.fairstandard.docs-site-build`, 04:30, 12:30, 20:30) runs `~/.claude/docs-site-build/run.sh`. It pulls each service repo's `main`, exports the OpenAPI spec, converts the markdown to MDX, runs `mint validate`, `mint broken-links`, and the anatomy check, has a reviewer model read the change summary, and pushes to `main`. Mintlify deploys on push. A change the reviewer holds lands on a `docs/<stamp>` branch as a draft PR with a Linear issue.

The full spec is `workflows/docs-site-build.md` in the repositories checkout.

## Working on it locally

```bash
npm i -g mint
export PATH=/opt/homebrew/opt/node@22/bin:$PATH   # mint refuses Node 25+
mint dev                                          # preview at localhost:3000
mint validate && mint broken-links
```

To regenerate the service pages by hand without pushing:

```bash
/bin/bash ~/.claude/docs-site-build/run.sh --dry-run
```

Tests for the build live next to it:

```bash
python3 -m pytest ~/.claude/docs-site-build/ -q
/bin/bash ~/.claude/docs-site-build/test.sh
```
