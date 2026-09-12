# Examples For `local_business_lead_finder`

## Low-Cost Test Examples

- Run a low-cost test with 5 coffee shops in Berlin and no reviews.

## Normal User Examples

- Find 50 dentists in Essen, Germany with websites and phone numbers using `local_business_lead_finder`.
- Find cafes in Berlin with rating above 4.3 and at least 100 reviews using `local_business_lead_finder`.
- Scrape 20 plumbers in Hamburg and enrich websites only after the first test run.

## Advanced Examples

- Chain `local_business_lead_finder` after a planning step and only run it once required inputs are present.
- Compare two possible `local_business_lead_finder` configurations and recommend the lower-cost option.

## Conditional Examples

- Ask for mode-specific fields only after the mode or action is selected.

## Validation And Error Examples

- If the API returns a validation error, identify the invalid field, correct the JSON, and retry once.
- If the first run times out, reduce scope, preserve the original goal, and retry with safer limits.

## Example JSON Input

```json
{
  "queries": [
    "dentist"
  ],
  "mode": "fast"
}
```
