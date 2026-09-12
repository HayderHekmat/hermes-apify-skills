# Hermes Apify Skills

Official example [Hermes Agent](https://hermes-agent.nousresearch.com/) skills generated from [Apify](https://apify.com/) Actors by **Solutions Smart**.

This repository is a free, public Hermes skills library.

The skill generator is available on Apify:

**Actor:** [solutionssmart/hermes-skill-builder-for-apify-apis](https://apify.com/solutionssmart/hermes-skill-builder-for-apify-apis)

> Not affiliated with unofficial GitHub mirrors that only copy Apify READMEs.
> Official Store listing: `apify.com/solutionssmart/...`
> Official skills repository: this repository.

## What you get

Each skill folder is a Hermes-ready package:

* `SKILL.md` — YAML frontmatter and instructions for Hermes 0.21.x
* `manifest.json`
* `input_schema.json`
* `tool_call_contract.json`
* `examples.md`
* `test_prompts.md`
* `integration_notes.md`

Apify-backed skills declare `APIFY_TOKEN` under `required_environment_variables`.

## Requirements

* [Hermes Agent](https://hermes-agent.nousresearch.com/) **v0.21.1+** — CLI or Desktop
* An [Apify](https://apify.com/) API token for skills that call Actors

Set the token in Hermes through CLI setup or `~/.hermes/.env`.

**Do not commit API tokens to this repository.**

## Install a skill

### Option A — Install one skill from GitHub

```bash
hermes skills install HayderHekmat/hermes-apify-skills/skills/fast_google_maps_scraper
```

### Option B — Add this repository as a tap

```bash
hermes skills tap add HayderHekmat/hermes-apify-skills
hermes skills search maps
hermes skills install HayderHekmat/hermes-apify-skills/fast_google_maps_scraper
```

### Option C — Manual copy

1. Clone or download this repository.
2. Copy the skill folder to your Hermes skills directory.

Examples:

**CLI default**

```text
~/.hermes/skills/automation/<skill-name>/
```

**Hermes Desktop on Windows**

```text
%LOCALAPPDATA%\hermes\skills\automation\<skill-name>\
```

3. Restart Hermes Desktop or open a **new chat**.
4. Run the skill's slash command, for example:

```text
/fast-google-maps-scraper
```

## Included skills

| Skill                      | Slash command               | Source Actor                                                                                       |
| -------------------------- | --------------------------- | -------------------------------------------------------------------------------------------------- |
| `fast_google_maps_scraper` | `/fast-google-maps-scraper` | [solutionssmart/fast-google-map-scraper](https://apify.com/solutionssmart/fast-google-map-scraper) |

More skills will be added as additional Apify Actors are published.

## Generate your own skill

1. Open [Hermes Skill Builder](https://apify.com/solutionssmart/hermes-skill-builder-for-apify-apis).
2. Paste an Apify Actor URL, OpenAPI spec, GitHub repository, or API documentation URL.
3. Use:

   * `targetFormat: hermes`
   * `exportZip: true`
   * `llmProvider: none`
4. Run the Actor.
5. Download the generated ZIP.
6. Install the skill using one of the methods above.

## How this differs from Hermes `/learn`

|                | Hermes `/learn`                                       | Hermes Skill Builder                                                  |
| -------------- | ----------------------------------------------------- | --------------------------------------------------------------------- |
| Best for       | Docs, notes, and workflows you already walked through | Apify Actors and APIs that need verified schemas                      |
| Output         | Agent-authored `SKILL.md`                             | Full skill package with `tool_call_contract` and cost-safety metadata |
| Apify metadata | Heuristic or docs-based                               | Official Actor metadata when available through `schemaVerified`       |

Use both where appropriate.

`/learn` is useful for procedures and knowledge captured through interaction. Hermes Skill Builder is designed for **Apify-verified executable skill packages**.

## Frontmatter notes

Generated skills targeting Hermes 0.21.x include:

* `name`
* `description` — up to 60 characters
* `version`
* `author`
* `license`
* `metadata.hermes` tags and category
* `required_environment_variables`
* `APIFY_TOKEN` for Apify-backed sources

### Platforms

Do **not** use:

```yaml
platforms: [hermes]
```

Hermes expects operating-system values such as:

```yaml
platforms:
  - macos
  - linux
  - windows
```

Alternatively, omit `platforms` entirely.

An invalid `platforms` value can prevent a skill from appearing in Hermes Desktop chat.

## Repository layout

```text
hermes-apify-skills/
├── README.md
└── skills/
    └── fast_google_maps_scraper/
        ├── SKILL.md
        ├── manifest.json
        ├── input_schema.json
        ├── tool_call_contract.json
        ├── examples.md
        ├── test_prompts.md
        └── integration_notes.md
```

## Links

* [Solutions Smart on Apify](https://apify.com/solutionssmart)
* [Hermes Skill Builder Actor](https://apify.com/solutionssmart/hermes-skill-builder-for-apify-apis)
* [Hermes Agent Skills documentation](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills)
* [Maintainer GitHub](https://github.com/HayderHekmat)

## License

MIT — see `LICENSE` if present.

Individual Apify Actors remain subject to their own Apify Store terms. This repository distributes generated skill packages and related documentation.

## Disclaimer

These skills help Hermes call Apify Actors.

You are responsible for:

* Apify usage costs
* Actor pricing
* Compliance with Apify terms
* Compliance with target website terms
* Applicable laws and regulations, including personal-data requirements such as GDPR
