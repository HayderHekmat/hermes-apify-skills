# Examples For `actorwebapp`

## Low-Cost Test Examples

- Run a low-cost test with 5 coffee shops in Berlin and no reviews.

## Normal User Examples

- Use `actorwebapp` for turn a crawler into a branded website data-collection tool.
- Prepare a valid input for `actorwebapp` using the real field names from `input_schema.json`.
- Run a normal workflow with `actorId` set to a realistic target.

## Advanced Examples

- Chain `actorwebapp` after a planning step and only run it once required inputs are present.
- Compare two possible `actorwebapp` configurations and recommend the lower-cost option.

## Conditional Examples

- Ask for mode-specific fields only after the mode or action is selected.

## Validation And Error Examples

- If the API returns a validation error, identify the invalid field, correct the JSON, and retry once.
- If the first run times out, reduce scope, preserve the original goal, and retry with safer limits.

## Example JSON Input

```json
{
  "actorId": "solutionssmart/brand-dna"
}
```
