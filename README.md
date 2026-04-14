# DebtSignal static site

Static landing page and conceptual API docs for DebtSignal.

## Local run

Serve the repo root with any static file server, for example:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Files

- `index.html` - single-page landing/docs site
- `styles.css` - responsive styling
- `docs/openapi.json` - OpenAPI 3.1 conceptual v1 schema
- `docs/sample-event.json` - coherent sample event payload
- `llms.txt` - concise agent-readable API summary

## Render deploy

- Build command: `echo 'Static site ready'`
- Publish path: `.`

No package manager files or external build tooling are required.
