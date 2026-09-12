# Test Prompts For `fast_google_maps_scraper`

## Basic Sanity Tests

1. Load `fast_google_maps_scraper` and summarize what it does.
2. Create a minimal valid input using `mode`.
3. Explain the expected output fields without running the workflow.

## Input Validation Tests

1. Try an empty input and ask for missing required fields.
2. Pass a wrong type for the first known field and explain the correction.
3. Include an unknown optional field and decide whether it can be safely ignored.

## Edge Case Prompts

1. The source service is rate limited. Describe the retry behavior.
2. The documentation does not specify an output schema. Return the safest structured response.
3. The user asks for a very large run. Recommend a small validation run first.

## Expected Behavior

The agent should validate inputs, avoid leaking secrets, use the source workflow conservatively, and return a clear summary plus structured output.
