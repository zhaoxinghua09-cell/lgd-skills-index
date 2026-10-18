# LGD Skills Ecosystem Registry

[![Made for GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-static--site-0078d4.svg)](https://zhaoxinghua09-cell.github.io/lgd-skills-index/)
[![Bilingual](https://img.shields.io/badge/i18n-English%20%7C%20中文-brightgreen.svg)](#)
[![Packages](https://img.shields.io/badge/registry-187%20packages-informational.svg)](#)
[![AI-protocol ready](https://img.shields.io/badge/AI%20protocol-187%2F187%20ready-2ea44f.svg)](#)
[![llms.txt](https://img.shields.io/badge/AI--friendly-llms.txt-101E2C.svg)](llms.txt)

> A zero-dependency, bilingual static registry: one open entry point to **187 governance-oriented agent skill packages**, organised across six practice lines, with search, filters and machine-readable data.

**Live site**: <https://zhaoxinghua09-cell.github.io/lgd-skills-index/>

This is a **GitHub Pages static-site repository** — no backend, no build step, no npm dependency. `index.html` in the root is the whole site: it embeds a `DATA` JSON (the skill registry plus a public-asset list), and a small amount of vanilla browser-side JavaScript renders the stat strip, per-line bars, a searchable/filterable skill table and public-asset cards.

## Features

- **187 packages in one open registry** (SK-001 … SK-187), each carrying a machine-readable SKILL.md contract (when-to-use / usage / workflow).
- **Six practice lines**: L1 Theory (38), L2 Product (22), L3 Evaluation (12), L4 Ecosystem (8), L5 Compliance (13), L6 Infrastructure (94).
- **Bilingual UI** (English + 中文), filtered and searchable by package name, slug or ID.
- **Honest public links**: a "Public entry" link is shown only where the source index verified a remote URL; staged packages show a neutral pending badge — no invented URLs.
- **Desensitised by default**: no local absolute paths, credentials or internal codenames appear on the page.
- **SEO-ready**: ships `robots.txt` and `sitemap.xml`.
- **Zero runtime**: open `index.html` and it works.

## Quick Start

No install required — a modern browser is enough.

```bash
git clone https://github.com/zhaoxinghua09-cell/lgd-skills-index.git
cd lgd-skills-index
start index.html        # Windows; use `open` on macOS, `xdg-open` on Linux
```

Or use the deployed site directly:

```text
https://zhaoxinghua09-cell.github.io/lgd-skills-index/
```

Then search by package name / slug / ID, filter by practice line, AI-protocol status or executability, and browse the verified public-asset cards.

## Examples

The registry is embedded as `var DATA = {...}` near the end of `index.html`. Extract it with a script:

```bash
python - <<'PY'
import re, json
html = open('index.html', encoding='utf-8').read()
data = json.loads(re.search(r'var DATA = (\{.*?\});\s*\nvar LINE_LABEL', html, re.S).group(1))
print('total:', data['stats']['total'])
print('published on ModelScope:', data['stats']['ms_published'])
PY
```

## Repository layout

```text
lgd-skills-index/
├── index.html            # the site (single render entry, embeds DATA JSON)
├── lgd-skills-index.html # legacy same-content copy
├── robots.txt            # crawler rules + sitemap pointer
├── sitemap.xml           # sitemap
├── README.md             # bilingual readme
├── README.en.md          # this file
├── llms.txt              # minimal index for AI agents
├── llms-full.txt         # full text for AI agents
├── AGENTS.md             # working guide for AI agents
├── SECURITY.md           # security policy
└── CONTRIBUTING.md      # contribution / errata guide
```

## License

**This repository currently ships no LICENSE file.** Each skill package / asset listed in `index.html` carries its own independent license (e.g. the per-package ModelScope repos, `silent-failure-catalog` under MIT + ARC, `lgd-theory` under CC-BY-4.0). This index site itself claims no additional copyright or licensing terms. Before reusing or redistributing data from this index, please contact the maintainer to confirm the position.

## Disclaimer

This page is an aggregated, descriptive registry of public skills; it does not warrant the quality, compliance or fitness of any listed package. External links, licenses and download counts follow the source snapshot dated 2026-10-16 and should be independently verified before citation. This repo contains no runnable backend logic.
