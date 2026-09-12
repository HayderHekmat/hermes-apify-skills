---
name: local_business_lead_finder
description: "Discover, extract, and enrich local business leads from"
version: 1.0.0
author: Hermes Skill Builder
license: NOASSERTION
required_environment_variables:
  - name: APIFY_TOKEN
    prompt: Apify API token
    help: https://console.apify.com/settings/integrations
    required_for: running Apify Actors
metadata:
  hermes:
    tags:
      - apify-actor
      - agent-skill
    category: developer-tools
    requires_toolsets: []
    requires_tools: []
---
# Local Business Lead Finder

Skill package: `local_business_lead_finder`

## What This Skill Does

Discover, extract, and enrich local business leads from Google Maps. Find businesses by keyword and location, collect contact details, emails, and social profiles, and export clean, deduplicated data. Built for automation, CRMs, and recurring lead generation workflows.

This skill is Hermes-ready and designed for Hermes Agent skill workflows. It is also compatible with skill-style agent systems that read markdown instructions, a manifest, and a JSON input schema.

## When To Use It

- Local Business Lead Finder (Google Maps Leads Scraper)
- Build prospect lists of local businesses for sales outreach and agency prospecting (e.g., plumbers, restaurants, clinics).
- Local SEO research: analyze competitors, business density, and presence by area.
- Market research: track businesses by geography and status over time.
- Scheduled lead refresh: run recurring discovery and only surface new or updated business leads.

## Inputs Expected From Normal Users

- `mode` (string) - Fast mode extracts leads only. Deep mode enables website enrichment within the configured limits.
- Advanced, internal, and cost-sensitive fields remain available in `input_schema.json`, but the agent should not ask about them by default.

## Output Expected

The workflow returns an array of records from the Actor's default Dataset.

Common record fields:

- `place_name` (string) - Business or place name when available.
- `address` (string) - Detected street address or location text when available.
- `website` (string) - Business website URL when available.
- `rating` (number) - Google Maps rating when available.

## Step-By-Step Workflow

1. Read the user's goal and map it to one of the detected capabilities.
2. Validate required inputs against `input_schema.json`.
3. Ask for missing required values before making any external call or Actor run.
4. Execute the documented API, repository tool, or Apify Actor workflow described by the source.
5. Return a concise summary, structured result data, and any relevant links or dataset references.
6. For long-running work, report progress and preserve enough context for retry.

## How This Skill Calls The Apify Actor

- Actor slug: `solutionssmart/local-business-lead-finder`
- Required secret: `APIFY_TOKEN`
- Start run endpoint: `https://api.apify.com/v2/acts/solutionssmart~local-business-lead-finder/runs`
- Run-sync endpoint: `https://api.apify.com/v2/acts/solutionssmart~local-business-lead-finder/run-sync-get-dataset-items`
- Expected result: dataset items from the default dataset
- Input schema source: `apify_actor_metadata`
- Readiness level: `executable`

## Before Running

- Verify `APIFY_TOKEN` exists in the agent secret store.
- Validate user input against `input_schema.json`.
- Use the run-sync endpoint for small jobs.
- Use the async run endpoint for larger jobs and then fetch dataset items.


## Required And Conditional Inputs

Always-required fields:

- `queries`

Conditional requirements depend on the selected mode, action, operation, or task:

- No high-confidence conditional requirements were inferred.


## Field Guidance For Agents

By default, the agent should only ask about agentDefaultFields. Advanced fields should be used only when the user explicitly requests expert control.

### Default Workflow

- Default mode: `fast`
- Ask first: `mode`

### Ask The User First

`mode`

### Conditional-Only Fields

none

These fields are valid and user-facing, but they should not be requested by default. Ask for them only when the user selects a mode, action, or operation that requires them.

Apply `conditionalRequirements` before asking for these fields.

### Ask Only If Needed

`language`, `emailScanDepth`, `detailConcurrency`, `enrichmentConcurrency`, `proxyMode`, `proxyCountryCode`

These are technical or expert options. Use them only when the user asks for advanced behavior or operational tuning.

### Do Not Ask Normal Users

`debug`

These are billing, debug, storage, telemetry, or internal fields. Normal users should not be asked about them.

### Cost-Sensitive Fields

`maxResultsTotal`, `enrichWebsite`, `emailScanDepth`, `maxWebsitesToEnrich`, `maxRunTimeSec`, `detailConcurrency`, `enrichmentConcurrency`, `proxyMode`, `proxyCountryCode`

These can increase runtime, compute, memory use, scraping depth, or external requests. Warn the user before enabling or increasing them.


## Cost-Safe Execution

- Risk level: `high`
- Recommended test input:

```json
{
  "queries": [
    "dentist"
  ],
  "mode": "fast"
}
```

- Safe defaults:

```json
{}
```

- High-cost fields: `maxResultsTotal`, `enrichWebsite`, `emailScanDepth`, `maxWebsitesToEnrich`, `maxRunTimeSec`, `detailConcurrency`, `enrichmentConcurrency`, `proxyMode`, `proxyCountryCode`

Agent guidance:

- Start with a small maxPlaces, maxItems, or maxResults value for test runs.
- Disable review scraping unless explicitly requested.
- Disable website enrichment for first validation runs.
- Use async runs for large jobs.


## Error Handling

- If an input is missing or ambiguous, ask a targeted follow-up question.
- If the source API or Actor returns a validation error, explain the failing field and suggest a corrected input.
- If rate limits or transient network errors occur, retry once with backoff and then report the failure clearly.
- If the source documentation is incomplete, state the assumption and keep raw response details visible.

## Safety And Rate-Limit Notes

- Respect the terms, robots policies, and rate limits of the source service.
- Do not expose API keys, Apify tokens, or personal data in logs or final answers.
- Prefer small test runs before large scraping or API jobs.
- Avoid browser rendering unless the workflow explicitly requires it.

## Example User Commands

- "Use `local_business_lead_finder` to run the default workflow for this source."
- "Generate a request for `local_business_lead_finder` using these parameters: ..."
- "Validate this `local_business_lead_finder` input before running it."
- "Retry the failed `local_business_lead_finder` operation and explain what changed."

## Integration Notes For Hermes Agent

Copy this folder into `~/.hermes/skills/<category>/local_business_lead_finder/` or install it with `hermes skills install <url>`. Keep `SKILL.md`, `manifest.json`, and `input_schema.json` together so the agent can load the instructions and validate user input.
