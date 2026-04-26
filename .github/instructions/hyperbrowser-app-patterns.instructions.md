---
applyTo: "**/*hyperbrowser*,**/app/api/**/route.ts,**/lib/hb.ts,**/lib/hyper.ts,**/lib/hyperbrowser.ts"
---

When building Hyperbrowser apps:

- Use `@hyperbrowser/sdk` server-side only.
- Load `HYPERBROWSER_API_KEY` from environment/config and never expose it to client code.
- Validate request bodies and URLs before browser automation starts.
- Bound crawl depth, page count, timeout, and content size.
- Use retry/backoff for transient browser and network failures.
- Clean up Hyperbrowser sessions in `finally` blocks when using session APIs.
- Return structured API responses with `success`, `data`, and `error` fields.
