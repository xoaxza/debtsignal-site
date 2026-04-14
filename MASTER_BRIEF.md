# DebtSignal launch master brief

Task ID: debtsignal-site-2026-04-14
Owner: conductor-agent
Status: active

User goal:
- Find unique Wall Street data that is very valuable but messy.
- Package it as an AI-agent-friendly API concept.
- Make a public website with API info/docs.
- Send an email to team@scottyshelpers.org with the website link and API information.

Chosen product direction:
- DebtSignal API
- A docs-first, AI-agent-friendly API concept for financing, covenant, waiver, maturity, and related agreement-change events disclosed in SEC 8-K filings and attached exhibits.

Why this direction:
- High-value workflow: debt raises, amendments, waivers, covenant changes, defaults, maturity extensions, refinancings, and related agreement changes are meaningful for credit investors, event-driven funds, diligence teams, and AI agents.
- Messy source data: financing disclosures are spread across 8-K items and exhibits, inconsistently worded, often buried in legal documents, and difficult to normalize across issuers.
- Clean commercial path: the primary source is SEC public data, which is more commercially workable than many licensed or restricted Wall Street datasets.
- Honest v1 scope: launch a source-linked event feed and docs-first site, not a full legal parser, covenant compliance engine, or live x402 billing product.

In scope:
- Publish or refresh a live Render-hosted website for DebtSignal.
- Include concise landing-page positioning and API docs.
- Include agent-friendly endpoint definitions, response-shape principles, sample JSON, provenance concepts, and caveats.
- Include x402-ready positioning for future monetization.
- Ensure the site is pushed to GitHub and deployed via Render.
- Send one email to team@scottyshelpers.org after the live URL is verified.

Out of scope:
- Full live extraction backend across SEC filings.
- Full x402 payment integration.
- Production billing/auth, SLAs, or enterprise security claims.
- Sending to any recipients other than team@scottyshelpers.org.

Acceptance criteria:
1. Research grounding
   - Site claims are grounded in public SEC sources and realistic product scope.
2. Product clarity
   - The website clearly explains what the data is, why it is valuable, why it is messy, who it is for, and what the API returns.
3. Agent friendliness
   - The docs include a minimal endpoint set, response-shape principles, sample JSON, and machine-readable artifacts where practical.
4. Deployment quality
   - The site is verified locally or by file checks, is pushed to GitHub, is deployed on Render, and the live URL is verified.
5. Email completeness
   - The email includes the live link, what DebtSignal does, why the dataset is valuable, example endpoint coverage, x402-ready positioning, and caveats.

Primary owner by task:
1. Research agent
   - Finalize the product thesis, source grounding, endpoint surface, response fields, use cases, and caveats for DebtSignal.
2. Marketing agent
   - Draft landing-page copy refinements and the outbound email copy for team@scottyshelpers.org.
3. Coding agent
   - Use Codex CLI to build or refine the static website and machine-readable docs files, verify them, push GitHub changes, and handle Render deployment/verification.
4. Conductor
   - Review specialist outputs, reconcile the final positioning, monitor milestone completion, and deliver the final user-facing handoff.

Definition of done:
- Live website exists on Render.
- Website includes product narrative, API info/docs, sample JSON, caveats, and x402-ready positioning.
- GitHub repo URL exists.
- Live URL is verified by direct fetch.
- Email is sent to team@scottyshelpers.org with the live link and API summary.
