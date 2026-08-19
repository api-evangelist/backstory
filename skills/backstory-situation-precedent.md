---
name: Find how we handled this situation before
description: >-
  Use Backstory's organizational deal history to find the closest precedents to
  the situation a rep is stuck in, and what the team actually did about them.
api: mcp/backstory-mcp.yml
surface: mcp
endpoint: https://mcp.people.ai/mcp
operations:
  - Find Account
  - Recent Opportunity Activity
  - Situation Search
  - Ask Sales AI About Account
generated: '2026-08-14'
method: generated
source: https://help.backstory.ai/en/articles/15252736-backstory-mcp
---

# Find how we handled this situation before

`Situation Search` is Backstory's precedent tool and it is marked **beta** by the
provider. It takes a described issue or challenge, builds a situational profile
from the deal's own activity, and returns **up to four** of the most similar
historical opportunities in the organization, ranked by how closely they match —
each with a situation profile, deal attributes (owner and amount), the actions
the team took, and the outcome.

## Steps

1. **Ground the situation in a real deal.** Resolve the account or opportunity
   first (`Find Account`, then `Recent Opportunity Activity`) so the situational
   profile is built from actual activity rather than from the user's paraphrase.
2. **Describe the situation plainly.** Call `Situation Search` with the obstacle
   in the user's own words — "stuck at procurement, legal wants custom terms",
   "third final-stage deal against this competitor". Specificity beats keywords.
3. **Report the precedents as evidence.** For each returned deal give: how it
   matched, owner and amount, what the team did, and how it ended. Do not
   average them into a single recommendation; the value is in the individual
   outcomes, including the ones that lost.
4. **Only then advise.** If the user wants a recommendation, call
   `Ask Sales AI About Account` for Backstory's own analysis and present it as a
   separate, labelled opinion alongside the precedents.

## Rules

- At most four precedents come back. If fewer return, say so — do not pad the
  list with deals from step 1 or from general knowledge.
- The tool is beta. Say that when you present its output.
- Precedents are drawn from the user's own organization and respect that user's
  record permissions; a deal they cannot see will not appear, so never present
  the result as an exhaustive history.

## Errors

See `errors/backstory-problem-types.yml`. A `401` means reconnect the connector;
an empty result set is a valid answer, not a failure to retry.
