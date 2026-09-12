# Examples For `amazon_price_rank_monitor`

## Low-Cost Test Examples

- Run a low-cost test with 5 coffee shops in Berlin and no reviews.

## Normal User Examples

- Use `amazon_price_rank_monitor` to monitor large Amazon ASIN lists for price changes.
- Prepare a valid input for `amazon_price_rank_monitor` using the real field names from `input_schema.json`.
- Run a normal workflow with `asins` set to a realistic target.

## Advanced Examples

- Use custom proxy settings for a difficult target site.
- Increase concurrency for a larger run after a successful test.
- Chain `amazon_price_rank_monitor` after a planning step and only run it once required inputs are present.
- Compare two possible `amazon_price_rank_monitor` configurations and recommend the lower-cost option.

## Conditional Examples

- Ask for mode-specific fields only after the mode or action is selected.

## Validation And Error Examples

- If the API returns a validation error, identify the invalid field, correct the JSON, and retry once.
- If the first run times out, reduce scope, preserve the original goal, and retry with safer limits.

## Example JSON Input

```json
{
  "marketplace": "amazon.com",
  "deduplicate": true,
  "onlyChanges": false,
  "maxConcurrency": 3,
  "maxRequestRetries": 6,
  "requestTimeoutSecs": 60
}
```
