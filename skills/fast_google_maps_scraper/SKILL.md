---
name: fast_google_maps_scraper
description: "Fast Google Maps Scraper agent skill"
version: 1.0.0
author: Hermes Skill Builder
license: NOASSERTION
required_environment_variables:
  - APIFY_TOKEN
metadata:
  hermes:
    tags:
      - apify-actor
      - agent-skill
    category: developer-tools
    requires_toolsets: []
    requires_tools: []
---
# Fast Google Maps Scraper

Skill package: `fast_google_maps_scraper`

## What This Skill Does

HTTP-first Google Maps scraper for search listings, place details, reviews, lead scoring, and optional website enrichment.

This skill is Hermes-ready and designed for Hermes Agent skill workflows. It is also compatible with skill-style agent systems that read markdown instructions, a manifest, and a JSON input schema.

## When To Use It

- Fast Google Maps Scraper
- Low-cost prospecting and lead generation from Google Maps business listings.
- Building lists of businesses with names, ratings, categories, addresses, coordinates, and place identifiers.
- Fetching full place details for lead qualification and outreach prioritization.
- Collecting and analyzing customer reviews for sentiment, volume, and per-place review datasets.
- Enriching business websites to extract emails, social links, page titles, and contact pages for outreach.
- Targeted local searches using city/country, structured geolocation fields, custom lat/long anchors, radius or GeoJSON points.

## Inputs Expected From Normal Users

- `mode` (string) - list searches only and is cheapest; place scrapes one known place ID; search lists places, fetches details, and optionally reviews.
- `query` (string) - Business/category query, for example 'dentists' or 'coffee shops'. Required for list and search mode.
- `searchLocation` (string) - Free-form location such as Berlin, Germany. Used together with the search query.
- `maxPlaces` (integer) - Maximum number of search results to list or fully scrape.
- `maxReviews` (integer) - Maximum reviews to fetch for each place. Set to 0 to skip reviews.
- `enrichWebsites` (boolean) - Fetch listed websites to extract title, description, emails, and social links.
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

- Actor slug: `solutionssmart/fast-google-map-scraper`
- Required secret: `APIFY_TOKEN`
- Start run endpoint: `https://api.apify.com/v2/acts/solutionssmart~fast-google-map-scraper/runs`
- Run-sync endpoint: `https://api.apify.com/v2/acts/solutionssmart~fast-google-map-scraper/run-sync-get-dataset-items`
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

- `mode`

Conditional requirements depend on the selected mode, action, operation, or task:

- When `mode` = `search`: require `query`, `searchLocation`. Search and list modes require a business/category query and a target location.
- When `mode` = `list`: require `query`, `searchLocation`. Search and list modes require a business/category query and a target location.
- When `mode` = `place`: require `placeId`. Place/detail mode requires a known place ID.


## Field Guidance For Agents

By default, the agent should only ask about agentDefaultFields. Advanced fields should be used only when the user explicitly requests expert control.

### Default Workflow

- Default mode: `search`
- Ask first: `mode`, `query`, `searchLocation`, `maxPlaces`, `maxReviews`, `enrichWebsites`

### Ask The User First

`mode`, `query`, `searchLocation`, `maxPlaces`, `maxReviews`, `enrichWebsites`

### Conditional-Only Fields

`placeId`

These fields are valid and user-facing, but they should not be requested by default. Ask for them only when the user selects a mode, action, or operation that requires them.

`placeId` should only be requested when the user chooses `mode` = `place` or asks to scrape a known Google Maps place by ID.

### Ask Only If Needed

`outputMode`, `geolocationParameters`, `customGeolocation`, `maxConcurrency`, `zoom`, `language`, `gl`, `delaySeconds`, `timeoutSeconds`, `proxyConfiguration`, `proxyUrl`, `websiteEnrichmentDepth`, `websiteTimeoutSeconds`

These are technical or expert options. Use them only when the user asks for advanced behavior or operational tuning.

### Do Not Ask Normal Users

`enableSqliteCheckpoint`, `sqlitePath`, `enableBillingEvents`

These are billing, debug, storage, telemetry, or internal fields. Normal users should not be asked about them.

### Cost-Sensitive Fields

`maxPlaces`, `maxReviews`, `maxTotalReviews`, `maxConcurrency`, `proxyConfiguration`, `proxyUrl`, `enrichWebsites`, `websiteEnrichmentDepth`

These can increase runtime, compute, memory use, scraping depth, or external requests. Warn the user before enabling or increasing them.


## Cost-Safe Execution

- Risk level: `high`
- Recommended test input:

```json
{
  "mode": "search",
  "query": "coffee shops",
  "searchLocation": "Berlin, Germany",
  "maxPlaces": 5,
  "maxReviews": 0,
  "enrichWebsites": false
}
```

- Safe defaults:

```json
{
  "maxPlaces": 5,
  "maxReviews": 0,
  "enrichWebsites": false
}
```

- High-cost fields: `maxPlaces`, `maxReviews`, `maxTotalReviews`, `maxConcurrency`, `proxyConfiguration`, `proxyUrl`, `enrichWebsites`, `websiteEnrichmentDepth`

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

- "Use `fast_google_maps_scraper` to run the default workflow for this source."
- "Generate a request for `fast_google_maps_scraper` using these parameters: ..."
- "Validate this `fast_google_maps_scraper` input before running it."
- "Retry the failed `fast_google_maps_scraper` operation and explain what changed."

## Integration Notes For Hermes Agent

Copy this folder into `~/.hermes/skills/<category>/fast_google_maps_scraper/` or install it with `hermes skills install <url>`. Keep `SKILL.md`, `manifest.json`, and `input_schema.json` together so the agent can load the instructions and validate user input.
