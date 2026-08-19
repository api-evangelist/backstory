---
name: Brief me on an account before a call
description: >-
  Pull a complete, defensible picture of one customer account from Backstory —
  who is engaged, what was actually said, what is happening at the company, and
  what the risks are — before a meeting.
api: mcp/backstory-mcp.yml
surface: mcp
endpoint: https://mcp.people.ai/mcp
operations:
  - Find Account
  - Recent Account Activity
  - Engaged People
  - Account Company News
  - Account Status
generated: '2026-08-14'
method: generated
source: https://help.backstory.ai/en/articles/15252736-backstory-mcp
---

# Brief me on an account before a call

Backstory exposes no REST API contract publicly. Its only machine-callable
surface is the hosted MCP server at `https://mcp.people.ai/mcp`. Every tool named
below is a real tool the provider documents in its "Backstory MCP" article —
none is invented. The live `tools/list` is OAuth-gated, so per-tool input schemas
are not published; call tools by name with plain-language arguments and let the
client's tool descriptions drive argument shape.

## Before you start

- The connector must already be authorized. Interactive clients complete an
  OAuth authorization-code + PKCE flow against `https://mcp.backstory.ai/authorize`;
  programmatic clients send `PAI-Client-Id` and `PAI-Client-Secret` headers
  (case-sensitive) issued by a Backstory administrator.
- You will only ever see records the authenticating user can already see in
  Backstory Engagement Dashboards. If a record comes back empty, that is a
  permission or data-existence answer, not an error to retry around.
- Activity coverage is documented as the last 30 days of communications.

## Steps

1. **Resolve the account.** Call `Find Account` with the company name
   ("Find TechCorp"). If you are starting from a CRM record id instead, call
   `Find Record by CRM ID` — it resolves a Salesforce-style id straight to the
   account or opportunity. Carry the resolved account forward; do not re-guess it.
2. **Read what actually happened.** Call `Recent Account Activity` for the emails
   and meetings on the account. Quote from these rather than summarising from
   memory — the point of Backstory is that the activity record is the evidence.
3. **Map the humans.** Call `Engaged People` to see which internal and external
   contacts are in recent communications. Note who has gone quiet; that absence
   is usually the finding.
4. **Add outside context.** Call `Account Company News` for earnings calls, SEC
   filings and public reporting on the customer. Keep this separate from
   first-party activity when you report — one is what they told you, one is what
   they told the market.
5. **Get the provider's own read.** Call `Account Status` for Backstory's summary
   of risks, sentiment, key topics and recommended next steps.

## Reporting rules

- Separate observed activity from AI-generated assessment. Steps 2–4 are record;
  step 5 is Backstory's analysis.
- Name the people and dates you are relying on so the brief can be checked.
- If `Find Account` returns nothing, say the account was not found or is not
  visible to this user. Do not fall back to general knowledge about the company
  and present it as Backstory data.

## Errors

A `401` with `error_code: missing_credentials` means the connector is not
authorized — reconnect, do not retry. A `401` with `invalid_token` means the
token expired; the client should clear stored tokens and re-register. See
`errors/backstory-problem-types.yml`.
