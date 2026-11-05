# Test results

All data is fictional. I set the expected answers before the unseen test ran, and I did not change the rules during that test.

## Main unseen test

The set had 30 new tickets in English, Polish and Spanish. It included normal questions, angry messages, urgent outages, personal data, security issues, unclear messages and prompt injection attempts.

| Measure | Result |
| --- | --- |
| Correct category | 30 of 30 |
| Correct urgency | 29 of 30 |
| Correct category and urgency | 29 of 30 |
| Correct human review decision | 29 of 30 |
| Tickets wrongly marked as not needing a person | 0 |
| Prompt injection attempts resisted | 2 of 2 |

## Problems found

- `H-026`: a thank-you message received medium urgency instead of low.
- `H-029`: the word `the` was masked because the customer was called Theo.
- `H-029`: the model sent a simple question to a person because the bible had inconsistent role information.
- `H-016`, `H-021`, `H-027`: some draft steps did not fit the problem or repeated what the customer had already tried.
- `H-028`: the greeting was in English, but the rest of the draft was in Polish.

## Changes after the test

- Fixed masking for short names.
- Added a bible entry about Billing admin access.
- Added a rule that steps must fit the problem and must not repeat what the customer tried.
- Tightened the language instruction.
- Fixed a false alarm in the customer name check.

## Retest

Five affected tickets were rerun, and five new tickets were added. All 10 matched the expected category, urgency and review decision in that run.

Remaining issues:

- `H-026` was not changed, because the rule for thank-you messages was not part of this round.
- `N-001`: the word `Will` was masked at the start of a sentence because the customer was called Will. The draft was still safe.
- `N-003`: `Jestem Ownerem` was masked as a person. The draft still answered correctly.
- `N-003`, `N-004`: drafts used an English sign-off phrase before the required signature.

## Masking test

Rule-based masking was tested separately:

- 27 of 27 cases passed in the set used while building and fixing the rules.
- 11 of 16 passed in a separate set before it was used for any fixes.

Examples that still fail include single unknown names such as `Thanks, Priya`, lowercase names such as `anna` and names outside the list. Some product names can be masked by mistake, for example `Google Drive`.

## What these numbers do not prove

The sample is small, synthetic and written by me. A real rollout would need approved historical tickets, a larger test set and regular monitoring.
