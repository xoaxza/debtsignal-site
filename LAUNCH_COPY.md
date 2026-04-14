# DebtSignal launch copy

## Recommended single-page architecture

1. Hero
2. Problem / why this data is hard
3. Product overview / what DebtSignal returns
4. Who it is for / use cases
5. Endpoint highlights
6. Sample response
7. x402-ready positioning
8. Caveats and limitations
9. CTA / docs-first close

---

## 1) Hero

### Headline
DebtSignal

### Subheadline
Financing and covenant events from SEC 8-K filings — structured for APIs, agents, and credit workflows.

### Supporting copy
DebtSignal is a docs-first API concept for tracking debt raises, amendments, waivers, defaults, maturity extensions, refinancings, and related financing disclosures buried in SEC 8-Ks and attached exhibits. We turn messy public filings into source-linked event records that machines can query and humans can verify.

### Primary CTA
Read the API docs

### Secondary CTA
View sample response

### Trust / qualifier line
Built on public SEC disclosures. Honest v1 scope: source-linked event extraction, not a full legal parser or covenant compliance engine.

---

## 2) Problem

### Section title
Why this data is valuable — and why it stays messy

### Body copy
Debt markets move on details that rarely arrive in clean tables. A new term loan, a covenant waiver, an upsized revolver, a maturity push, a default notice, or an amendment to collateral terms can materially change credit risk and valuation.

But the underlying disclosures are fragmented. Relevant facts may appear across 8-K items such as 1.01, 2.03, 2.04, or 8.01, then continue into exhibit indexes, credit agreements, amendments, indentures, guarantee documents, or waiver letters. The wording is inconsistent. Key terms may be spread over dozens of pages. Important context is often disclosed in legal prose rather than in machine-readable form.

That makes financing events expensive to monitor at scale. Analysts read filings manually. Research pipelines miss nuance. Agents need structured fields, source links, and a clear confidence model — not just raw text.

### Problem bullets
- High-value events are often disclosed in long-form legal documents.
- The same concept can be described differently across issuers and filings.
- Key terms may sit in exhibits rather than the 8-K body.
- Buyers need speed, provenance, and enough structure to automate triage.

---

## 3) Product overview

### Section title
What DebtSignal does

### Body copy
DebtSignal is an AI-agent-friendly API for financing and covenant event detection in SEC 8-K filings and related exhibits. Each event is designed to return:

- issuer identity and filing metadata
- event type classification
- normalized financing details when extractable
- source excerpts and filing links for verification
- confidence and completeness signals

### Short value proposition
Use DebtSignal to screen filings faster, trigger research workflows, enrich diligence pipelines, and route only the highest-signal situations to human review.

### Product thesis block
The thesis is simple: financing disclosures are public, important, and operationally painful. A source-linked event feed creates immediate value even before full legal parsing is solved. Start with event detection and provenance. Expand into deeper term extraction over time.

---

## 4) Use cases

### Section title
Who it is for

### Use case 1
Credit and event-driven funds
Monitor new debt issuance, amendments, waivers, defaults, refinancings, and maturity changes across issuers without reading every filing end to end.

### Use case 2
Diligence and private credit teams
Surface debt-related disclosure history during underwriting, portfolio monitoring, and borrower review. Use source links to jump directly into the relevant filing or exhibit.

### Use case 3
Fintech and AI-agent builders
Trigger downstream workflows when a borrower discloses a covenant change, financing amendment, or default-related event. Feed normalized records into copilots, alerts, and internal tooling.

### Use case 4
Research and data engineering teams
Backfill a financing-event timeline, compare issuer disclosure patterns, and join event data with market, fundamental, or portfolio datasets.

---

## 5) Endpoint highlights

### Section title
Minimal endpoint surface, built for agents

### Intro copy
The API should stay compact in v1: a small set of endpoints, stable response shapes, and explicit provenance on every record.

### Endpoint 1
GET /v1/events

Purpose:
List financing and covenant-related events extracted from SEC 8-K filings.

Suggested filters:
- issuer
- cik
- ticker
- event_type
- filing_date_gte
- filing_date_lte
- accession_number
- has_exhibit
- min_confidence
- limit
- cursor

Returns:
A paginated list of normalized event objects with issuer, filing, classification, timestamps, and source references.

### Endpoint 2
GET /v1/events/{event_id}

Purpose:
Fetch one event with a richer extraction payload.

Returns:
- event classification
- extracted terms
- source excerpts
- filing URL
- exhibit references
- extraction notes
- confidence / completeness flags

### Endpoint 3
GET /v1/issuers/{issuer_id}/events

Purpose:
Retrieve an issuer timeline of financing disclosures.

Returns:
Chronological event history for one issuer, useful for borrower monitoring and diligence views.

### Endpoint 4
GET /v1/event-types

Purpose:
Expose the classification vocabulary used by DebtSignal.

Suggested initial event types:
- new_financing
- amendment
- waiver
- default_or_acceleration
- covenant_change
- maturity_extension
- refinancing
- repayment_or_termination
- collateral_or_guarantor_change
- liquidity_update

### Endpoint 5
GET /v1/docs/openapi.json

Purpose:
Machine-readable schema for agent integration, code generation, and documentation tooling.

### Response-shape principles
- Every record should include a stable event_id.
- Every extraction should include source_url and source_text or excerpt references.
- Fields that are not confidently extractable should be null, not guessed.
- Confidence and completeness should be explicit metadata, not implied certainty.

---

## 6) Sample response idea

### Section title
Example event object

```json
{
  "event_id": "evt_8k_0000123456_2026_04_10_001",
  "issuer": {
    "name": "Example Holdings, Inc.",
    "ticker": "EXH",
    "cik": "0000123456"
  },
  "filing": {
    "form": "8-K",
    "filed_at": "2026-04-10T20:12:00Z",
    "accession_number": "0000123456-26-000111",
    "filing_url": "https://www.sec.gov/Archives/...",
    "items": ["1.01", "2.03", "8.01"]
  },
  "event_type": "amendment",
  "title": "Second amendment extends revolving credit facility maturity",
  "summary": "Issuer entered into an amendment to its revolving credit agreement extending maturity and revising leverage covenant thresholds.",
  "extracted_terms": {
    "facility_type": "revolving_credit_facility",
    "maturity_date_old": "2027-06-30",
    "maturity_date_new": "2029-06-30",
    "principal_amount_usd": 750000000,
    "covenant_changes": [
      "maximum net leverage ratio increased for Q2-Q4 2026"
    ],
    "guarantor_change": null,
    "default_status": null
  },
  "sources": [
    {
      "document_type": "8-K",
      "source_url": "https://www.sec.gov/Archives/...",
      "excerpt": "On April 9, 2026, the Company entered into a Second Amendment..."
    },
    {
      "document_type": "Exhibit 10.1",
      "source_url": "https://www.sec.gov/Archives/...",
      "excerpt": "The Revolving Credit Maturity Date is hereby amended to June 30, 2029..."
    }
  ],
  "confidence": {
    "event_type": 0.97,
    "term_extraction": 0.81,
    "overall": 0.88
  },
  "completeness": {
    "core_event_detected": true,
    "key_terms_partial": true,
    "manual_review_recommended": true
  }
}
```

### Sample-response explainer
The important point is not perfect extraction of every legal term on day one. The value is a reliable event object with provenance, enough normalized fields for triage, and a fast path back to the original filing.

---

## 7) x402-ready positioning

### Section title
Built for open access now, x402-ready later

### Body copy
DebtSignal is launching as a docs-first product concept around public SEC data and developer-friendly schemas. Monetization and paid access can be layered in later.

The API is being designed to be x402-ready, meaning usage-based or agent-mediated payment flows can be added without changing the core event model. That is roadmap positioning, not a claim that billing or payment infrastructure is live today.

### Short version
Public-data API now. x402-ready architecture later.

---

## 8) Caveats and limitations

### Section title
Important caveats

### Body copy
DebtSignal should be explicit about what it does not yet do.

### Caveat bullets
- DebtSignal is not a legal opinion, covenant compliance engine, or substitute for reading source documents.
- Coverage is limited to publicly disclosed financing and covenant events that appear in SEC filings and available exhibits.
- The launch posture is docs-first: response examples describe the intended API shape and product direction, not a claim of exhaustive live extraction coverage across all issuers.
- Not every issuer discloses with the same detail, timing, or terminology.
- Some filings contain partial information, cross-references, redactions, or hard-to-parse exhibit language.
- Extracted terms may be incomplete or null when the source is ambiguous.
- Event classification and term extraction may require human review for high-stakes workflows.
- x402 positioning refers to future payment-readiness, not live billing or access control.
- v1 should be presented as a source-linked monitoring layer, not a complete debt intelligence platform.

### Honest footer line
If the choice is between overstating certainty and showing the source, show the source.

---

## 9) CTA

### Section title
Start with the filing, not the hype

### Body copy
If you build for credit, diligence, or agentic research, DebtSignal gives you a cleaner starting point: structured financing events, source-linked evidence, and a schema that can plug into real workflows.

### Primary CTA
Explore the docs

### Secondary CTA
Request early access

### CTA qualifier
Docs-first launch. Feedback from funds, fintech teams, and research builders is welcome.

---

## Optional short homepage version

### One-line descriptor
DebtSignal turns financing and covenant disclosures from SEC 8-K filings into source-linked event data for APIs, agents, and credit research.

### Three feature cards
1. Source-linked events
Track amendments, waivers, defaults, refinancings, and maturity changes with direct links back to the filing and exhibit.

2. Agent-friendly schema
Stable JSON, explicit nulls, confidence metadata, and machine-readable docs for automation.

3. Honest scope
Built for fast monitoring and triage today — not marketed as a full legal parser or covenant engine.
