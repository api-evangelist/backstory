---
name: Review a deal for risk and qualification
description: >-
  Pressure-test one opportunity in Backstory — what changed, who stopped
  responding, whether it is qualified against the methodology, and what to do
  next.
api: mcp/backstory-mcp.yml
surface: mcp
endpoint: https://mcp.people.ai/mcp
operations:
  - Top Records
  - Find Record by CRM ID
  - Recent Opportunity Activity
  - Scorecard
  - Opportunity Status
  - Ask Sales AI About Opportunity
generated: '2026-08-14'
method: generated
source: https://help.backstory.ai/en/articles/15252736-backstory-mcp
---

# Review a deal for risk and qualification

All tools below are documented Backstory MCP tools. The server is
`https://mcp.people.ai/mcp`; it is OAuth-protected and returns only records the
authenticating user can already see.

## Steps

1. **Pick the deal.** If the user named one, resolve it with
   `Find Record by CRM ID` (when they gave an id) or `Find Account` and work down
   to the opportunity. If they asked "what needs my attention", call
   `Top Records` — it returns the accounts and opportunities Backstory ranks
   highest on engagement, filters and admin-defined prioritization.
2. **Read the deal's own record.** Call `Recent Opportunity Activity` for the
   communications and meetings tied to that opportunity. Look for the last
   inbound message from the customer side and who sent it.
3. **Check qualification.** Call `Scorecard` to retrieve the Closeplan or
   qualification scorecard — the questions and the answers actually recorded
   (MEDDICC or whatever template the org runs). Report unanswered questions as
   unanswered; an empty scorecard field is a finding.
4. **Get the deal-level summary.** Call `Opportunity Status` for risks, momentum
   and suggested actions.
5. **Interrogate it.** Call `Ask Sales AI About Opportunity` with the specific
   question the user actually has ("what's blocking this deal?", "who has buying
   power here?"). This tool reasons over the full deal context; use it for the
   judgement call, not for retrieving facts you could have fetched in step 2.

## Reporting rules

- Lead with what changed and when, then who is missing, then the recommendation.
- Distinguish "no activity recorded" from "no activity happened" — Backstory sees
  captured email, meetings, calls, chat and transcripts, within a 30-day window.
- Never assert a close date, amount or stage that did not come back from a tool.

## Errors

Unauthorized responses are `401` with a Bearer challenge; see
`errors/backstory-problem-types.yml`. Backstory documents no idempotency
contract and no rate limits, so treat every call as a plain read and do not build
retry storms.
