# Hyperbrowser SDK Patterns

## Client Construction

```ts
import { Hyperbrowser } from '@hyperbrowser/sdk';

const hb = new Hyperbrowser({ apiKey: process.env.HYPERBROWSER_API_KEY! });
```

Only construct the client server-side. For build-safe Next.js modules, export `null` when the key is absent and return a structured API error at request time.

## Retry Wrapper

Use bounded exponential backoff for transient browser/network failures. Keep maximum retries and delays explicit.

## Scrape Pattern

```ts
const scrape = await hb.scrape.startAndWait({
  url,
  scrapeOptions: {
    formats: ['html'],
    timeout: 60000,
    waitFor: 5000,
  },
  sessionOptions: {
    useStealth: true,
    adblock: true,
  },
});
```

Check expected result fields before using them and return a typed error if missing.

## Crawl Pattern

Use a bounded URL queue:

- `maxPages`
- `depth`
- `sameDomainOnly`
- `includePatterns`
- `excludePatterns`
- file/login/mailto/tel skip patterns

Store completed and failed URLs separately so partial success is visible.

## Session Pattern

For generated tools or interactive workflows:

1. `sessions.create()`
2. `sessions.navigate()`
3. one or more actions: click, type, select, evaluate, screenshot, getHTML
4. `sessions.delete()` or stop/cleanup in `finally`

## Next.js API Route Pattern

- Parse `await request.json()` through a schema.
- Check server-side env vars before work starts.
- Wrap Hyperbrowser calls in retry/backoff.
- Return `{ success: true, data }` or `{ success: false, error }`.
- Log server errors internally but return sanitized messages.
