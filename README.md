# EveryInfra Analysis Skills

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/hero-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="assets/hero-light.svg">
    <img alt="Eight synthetic reviews are grouped into pain points and praise, each share written with its denominator, and the sample mean is set against the listing rating with a note." src="assets/hero-light.svg" width="100%">
  </picture>
</p>

<p align="center">
  <a href="https://github.com/everyinfra/analysis-skills/releases/latest"><img src="https://img.shields.io/badge/Download_latest_release-2F363D?style=for-the-badge&logo=github&logoColor=white" alt="Download the latest release"></a>
  <a href="https://github.com/everyinfra/analysis-skills/issues"><img src="https://img.shields.io/badge/Report_an_issue-2F363D?style=for-the-badge&logo=github&logoColor=white" alt="Report an issue"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/version-0.4.1-brightgreen" alt="version 0.4.1">
  <img src="https://img.shields.io/badge/license-Apache--2.0-brightgreen" alt="Apache-2.0">
  <img src="https://img.shields.io/badge/skills-6-brightgreen" alt="6 skills">
  <img src="https://img.shields.io/badge/model-your_own-brightgreen" alt="model">
</p>

<p align="center"><b>English</b> · <a href="README.zh-CN.md">简体中文</a> · <a href="README.es.md">Español</a></p>

**Free to download. Use your own AI tool and model.**

EveryInfra Analysis Skills is version `0.4.1`, licensed under Apache-2.0. The package is free to download and install. It ships **six** analysis Skills — four domain skills plus a shared **analysis-foundation** discipline layer. It does not call a model, does not bundle a model provider, and has no API key or runtime dependency. The customer's compatible AI tool supplies the model and the model quota.

A separate EveryInfra data-collection API or MCP call may cost money. Free Skill installation is not free collection.

## Skills

| Slug | What it analyzes |
| --- | --- |
| `ecommerce-product-analysis` | Product candidates from user-supplied CSV/JSON or results already fetched. |
| `social-content-performance` | Social content for a stated sample and time window, from supplied files or results already fetched. |
| `content-analysis-tagging` | Records labeled with a user-provided or agreed taxonomy. |
| `review-insights` | Pain points, praise, and rating patterns in product, app, place, or company reviews, from supplied files or results already fetched. |
| `spreadsheet-deliverable` | Editable .xlsx workbooks with live formulas (inputs/calculations/outputs separated, recalculation and error scan, built-in checks, assumptions with sources) |
| `analysis-foundation` | **Shared discipline layer**: four-step pipeline, numbers-from-code, denominator naming, n<30 no rates, uncertainty, causation wording, chart-choice table, method notes, LLM-labeling calibration. |

Each Skill analyzes supplied files or already-fetched results. Installing a Skill does not collect data.

## Use with EveryInfra data

Each Skill also works on results you already fetched from EveryInfra. Examples of matching EveryData actions (the live catalog lists current actions and fields):

| Skill | Example EveryData actions |
| --- | --- |
| `ecommerce-product-analysis` | `amazon/search`, `aliexpress/search`, `taobao/search`, `jd/search`, `shopee/search` |
| `social-content-performance` | `tiktok/search`, `tiktok/user_videos`, `youtube/search`, `xiaohongshu/search`, `bilibili/search` |
| `content-analysis-tagging` | Text records such as `xiaohongshu/search`, `reddit/search`, `zhihu/search`, or `comments` results |
| `review-insights` | `amazon/reviews`, `walmart/reviews`, `taobao/reviews`, `trustpilot/reviews`, `app_store/reviews`, `google_maps_reviews/reviews` |

Live catalog: `GET https://api.everyinfra.com/api/v1/social/catalog`.

## Quick start

1. Choose the Skill for the task.
2. Download the repository ZIP or clone `https://github.com/everyinfra/analysis-skills.git`. Install the selected Skill folder to the compatible host's documented Skill location. This README names `~/.agents/skills/` and `~/.claude/skills/`.
3. Configure or select the customer's own model in the AI host's own settings. The package does not configure the host and does not provide a model key.
4. Open the matching synthetic fixture. Give the Skill the fixture's `source_response` and task. The fixture includes `expected_output`; compare the returned structure, not exact model wording. This step makes no EveryInfra data-collection call.
5. For new data collection, see the live API/MCP documentation. Collection is separate and may be billable.

## Download

Obtain the repository source ZIP from the GitHub repository page:

1. Open [https://github.com/everyinfra/analysis-skills](https://github.com/everyinfra/analysis-skills).
2. Use GitHub **Code** → **Download ZIP**.
3. Unpack the ZIP.

Or clone `https://github.com/everyinfra/analysis-skills.git`.

## Install

| Host              | Install Directory       |
|-------------------|-------------------------|
| Codex CLI / IDE   | `~/.agents/skills/`     |
| Claude Code       | `~/.claude/skills/`     |

Copy one or more of these exact Skill folders into `~/.agents/skills/` or `~/.claude/skills/`:

- `skills/ecommerce-product-analysis`
- `skills/social-content-performance`
- `skills/content-analysis-tagging`
- `skills/review-insights`
- `skills/spreadsheet-deliverable`

Also copy `skills/analysis-foundation`: every Skill links to it as the shared discipline layer. Compatible hosts can use their own documented Skill folder.

Codex CLI / IDE: `$ecommerce-product-analysis` · `$social-content-performance` · `$content-analysis-tagging` · `$review-insights`

Claude Code: `/ecommerce-product-analysis` · `/social-content-performance` · `/content-analysis-tagging` · `/review-insights`

For a synthetic example, give the model only `source_response` and `task`; retain `expected_output` outside the model input to compare afterward.

[Build skills — Codex](https://developers.openai.com/codex/build-skills) · [Extend Claude with skills](https://code.claude.com/docs/en/skills)

## Synthetic fixtures

The `examples/` directory contains four synthetic fixtures, one per Skill. They are synthetic:

- `examples/ecommerce-product-analysis.synthetic.json`
- `examples/social-content-performance.synthetic.json`
- `examples/content-analysis-tagging.synthetic.json`
- `examples/review-insights.synthetic.json`

Open the matching fixture and give the Skill the fixture's `source_response` and task. Each fixture includes `expected_output`. Compare the returned structure, not exact model wording. Using a fixture makes no EveryInfra data-collection call.

## Collection and public API

Analysis in these Skills is free of Skill charges. Collection through EveryInfra API or MCP is a separate step and may be billable. Catalog or tool discovery does not grant permission to make a paid data call.

Public API references:

- [https://api.everyinfra.com/docs](https://api.everyinfra.com/docs)
- [https://api.everyinfra.com/openapi.json](https://api.everyinfra.com/openapi.json)

## Maintenance and feedback

Maintainer: EveryInfra (the organization).

Update triggers: public API contract or schema changes, a verified correction to a Skill or example, or an accepted user request. At each package version update, review open feedback before changing the manifest version and changelog. This is an event-driven manual cadence.

Feedback channel: public GitHub Issues at [https://github.com/everyinfra/analysis-skills/issues](https://github.com/everyinfra/analysis-skills/issues). Do not post API keys, credentials, private customer records, or other confidential data.

## License

Apache-2.0. See `LICENSE`.
