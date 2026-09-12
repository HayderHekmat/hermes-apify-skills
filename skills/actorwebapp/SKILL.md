---
name: actorwebapp
description: "Turn a compatible Apify Actor into a branded web app with a"
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
# ActorWebApp

Skill package: `actorwebapp`

## What This Skill Does

Turn a compatible Apify Actor into a branded web app with a simple input form, run status, Dataset results, exports, and shareable Standby URL. Give customers and teammates an easier way to use your Actor without exposing your API token.

This skill is Hermes-ready and designed for Hermes Agent skill workflows. It is also compatible with skill-style agent systems that read markdown instructions, a manifest, and a JSON input schema.

## When To Use It

- Turn a crawler into a branded website data-collection tool.
- Give customers a simple interface for a lead-generation or research Actor.

## Inputs Expected From Normal Users

- Advanced, internal, and cost-sensitive fields remain available in `input_schema.json`, but the agent should not ask about them by default.

## Output Expected

The workflow returns an array of records from the Actor's default Dataset.

Common record fields:

- Each returned record contains the fields provided by the source Actor.

## Step-By-Step Workflow

1. Read the user's goal and map it to one of the detected capabilities.
2. Validate required inputs against `input_schema.json`.
3. Ask for missing required values before making any external call or Actor run.
4. Execute the documented API, repository tool, or Apify Actor workflow described by the source.
5. Return a concise summary, structured result data, and any relevant links or dataset references.
6. For long-running work, report progress and preserve enough context for retry.

## How This Skill Calls The Apify Actor

- Actor slug: `solutionssmart/actorwebapp`
- Required secret: `APIFY_TOKEN`
- Start run endpoint: `https://api.apify.com/v2/acts/solutionssmart~actorwebapp/runs`
- Run-sync endpoint: `https://api.apify.com/v2/acts/solutionssmart~actorwebapp/run-sync-get-dataset-items`
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

- `actorId`

Conditional requirements depend on the selected mode, action, operation, or task:

- No high-confidence conditional requirements were inferred.


## Field Guidance For Agents

By default, the agent should only ask about agentDefaultFields. Advanced fields should be used only when the user explicitly requests expert control.

### Default Workflow

- Default mode: `not inferred`
- Ask first: none

### Ask The User First

none

### Conditional-Only Fields

none

These fields are valid and user-facing, but they should not be requested by default. Ask for them only when the user selects a mode, action, or operation that requires them.

Apply `conditionalRequirements` before asking for these fields.

### Ask Only If Needed

none

These are technical or expert options. Use them only when the user asks for advanced behavior or operational tuning.

### Do Not Ask Normal Users

none

These are billing, debug, storage, telemetry, or internal fields. Normal users should not be asked about them.

### Cost-Sensitive Fields

none

These can increase runtime, compute, memory use, scraping depth, or external requests. Warn the user before enabling or increasing them.


## Cost-Safe Execution

- Risk level: `low`
- Recommended test input:

```json
{
  "actorId": "solutionssmart/brand-dna"
}
```

- Safe defaults:

```json
{}
```

- High-cost fields: none

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

- "Use `actorwebapp` to run the default workflow for this source."
- "Generate a request for `actorwebapp` using these parameters: ..."
- "Validate this `actorwebapp` input before running it."
- "Retry the failed `actorwebapp` operation and explain what changed."

## Integration Notes For Hermes Agent

Copy this folder into `~/.hermes/skills/<category>/actorwebapp/` or install it with `hermes skills install <url>`. Keep `SKILL.md`, `manifest.json`, and `input_schema.json` together so the agent can load the instructions and validate user input.
