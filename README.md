# DebtSignal static site

Static landing page and machine-readable documentation for the DebtSignal API concept.

DebtSignal is presented here as a docs-first interface for source-linked financing and covenant event data derived from SEC 8-K filings and related exhibits. This repo does not represent a live production extraction backend. It is an evaluation artifact for the schema, payload shape, and product framing.

## Scope

- Focus: financing and covenant-related event records with provenance, timeline metadata, explicit nulls, and machine-readable errors.
- Source posture: public SEC disclosures only.
- Product maturity posture: conceptual docs and sample payloads, not a claim of exhaustive live coverage or production extraction operations.
- x402 posture: future-facing compatibility only. No live billing or access control is implemented in this static site.

## Local run

Serve the repo root with any static file server, for example:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Machine-readable artifacts

- `docs/openapi.json` - primary OpenAPI 3.1 contract
- `docs/openapi.yaml` - YAML mirror of the same contract
- `docs/sample-event.json` - sample single-event response matching the contract
- `llms.txt` - short agent-readable summary
- `llms-full.txt` - expanded agent-readable guidance

## Contract principles

- Stable envelopes: success responses use `data`, `meta`, and where relevant `page`.
- Cursor pagination: `page.next_cursor` is opaque and can be null.
- Provenance first: event records carry filing references, exhibit metadata, source excerpts, and extraction notes.
- Time semantics are explicit: filing timestamps are separate from event-effective dates and date precision.
- Explicit nulls: unknown or ambiguous terms remain `null`.
- Machine-readable errors: `400`, `402`, `429`, and `503` use problem-detail responses.

## Conceptual endpoint surface

- `GET /v1/docs/openapi.json`
- `GET /v1/events`
- `GET /v1/events/{event_id}`
- `GET /v1/event-types`

## Render deploy

- Build command: `echo 'Static site ready'`
- Publish path: `.`

No package manager files or external build tooling are required.
