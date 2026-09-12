# Examples For `co_star_real_estate_scraper`

## Low-Cost Test Examples

- Run a low-cost test with 5 coffee shops in Berlin and no reviews.

## Normal User Examples

- Use `co_star_real_estate_scraper` for coStar Real Estate Scraper.
- Prepare a valid input for `co_star_real_estate_scraper` using the real field names from `input_schema.json`.
- Run a normal workflow with `startUrls` set to a realistic target.

## Advanced Examples

- Use custom proxy settings for a difficult target site.
- Increase concurrency for a larger run after a successful test.
- Chain `co_star_real_estate_scraper` after a planning step and only run it once required inputs are present.
- Compare two possible `co_star_real_estate_scraper` configurations and recommend the lower-cost option.

## Conditional Examples

- Ask for mode-specific fields only after the mode or action is selected.

## Validation And Error Examples

- If the API returns a validation error, identify the invalid field, correct the JSON, and retry once.
- If the first run times out, reduce scope, preserve the original goal, and retry with safer limits.

## Example JSON Input

```json
{
  "maxItems": 5
}
```
