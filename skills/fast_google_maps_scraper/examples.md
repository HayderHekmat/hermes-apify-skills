# Examples For `fast_google_maps_scraper`

## Low-Cost Test Examples

- Run a low-cost test with 5 coffee shops in Berlin and no reviews.

## Normal User Examples

- Find 50 dentists in Essen, Germany with websites and phone numbers using `fast_google_maps_scraper`.
- Find cafes in Berlin with rating above 4.3 and at least 100 reviews using `fast_google_maps_scraper`.
- Scrape 20 plumbers in Hamburg and enrich websites only after the first test run.

## Advanced Examples

- Use custom proxy settings for a difficult target site.
- Increase concurrency for a larger run after a successful test.
- Chain `fast_google_maps_scraper` after a planning step and only run it once required inputs are present.
- Compare two possible `fast_google_maps_scraper` configurations and recommend the lower-cost option.

## Conditional Examples

- Scrape one known Google Maps place by `placeId` only when `mode` is `place`.

## Validation And Error Examples

- If `mode` is `search` but `query`, `searchLocation` is missing, ask the user for the missing field.
- If `mode` is `list` but `query`, `searchLocation` is missing, ask the user for the missing field.
- If `mode` is `place` but `placeId` is missing, ask the user for the missing field.
- If the API returns a validation error, identify the invalid field, correct the JSON, and retry once.
- If the first run times out, reduce scope, preserve the original goal, and retry with safer limits.

## Example JSON Input

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
