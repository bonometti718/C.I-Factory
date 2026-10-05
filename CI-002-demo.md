# C.I. #02 — Agent Economic Action Gate: reproducible demo

An AI agent can pay for a verifier, use an alternative, or continue without buying. Agent Economic Action Gate compares modeled expected values and returns `BUY`, `SKIP`, `STOP` or `ESCALATE`, plus a break-even price ceiling.

**Synthetic estimates, actual core outputs.** These six examples were executed against the local C.I. #02 implementation on 5 October 2026. They are not invented response examples, measured business outcomes, fresh marketplace calls or completed purchases. The exact source hashes are in `provenance.json`.

## Open and reproduce

- [Download the complete demo](CI-002-demo.zip), extract it and open `CI-002-demo/demo.html`.
- Select among six recorded cases to inspect full inputs and actual outputs.
- Run `python verify.py` in the extracted folder. This independent Python checker verifies the recorded calculations; it does not call or replace the production API.
- Watch `walkthrough.mp4`, a 60-second explanation of the recorded examples, not a live marketplace screen recording.
- [Contract and API quickstarts](capabilities/CI-002.md).

## The decision changes when the economics change

| Case | Decision | Action EV (USD) | Best outside EV (USD) | Price ceiling (USD) |
|---|---|---:|---:|---:|
| USD 3 verifier | BUY | 62 | 58 | 7 |
| USD 7 verifier: exact tie | SKIP | 58 | 58 | 7 |
| USD 8 verifier | SKIP | 57 | 58 | 7 |
| Confidence reduced to 0.79 | ESCALATE | 62 | 58 | 7 |
| Task success payoff set to zero | STOP | -3 | 0 | 0 |
| Free alternative with success probability 0.70 | SKIP | 62 | 70 | 0 |

The first example assumes a USD 100 net payoff on success, zero payoff on failure, a 0.50 baseline success probability and a 0.15 probability increase from the action. Its total modeled success probability is 0.65.

- Baseline expected value: `100 × 0.50 = 50`.
- Action expected value: `100 × 0.65 − 3 = 62`.
- Alternative expected value: `100 × 0.60 − 2 = 58`.
- Action advantage over the best outside option: `62 − 58 = 4`.
- Break-even price ceiling: `65 − 58 = 7`.

**A USD 7 ceiling does not mean BUY at USD 7.** BUY requires strictly better positive expected value. Ties prefer no purchase. A low or missing confidence value produces ESCALATE before the economic decision; confidence is a caller-supplied reliability gate, not a calibrated probability multiplier.

## Verification performed

All six cases passed independent checks for decisions, reasons, recommendations, confidence, action probability, seven economic values, break-even flags and alternative comparisons. The actual core also rejected an input where baseline plus action probability delta exceeded one. The existing implementation test suite passed **19 tests**, including decimal ties, invalid inputs, 500 cost cases, mocked billing/resume behavior, local HTTP access controls, MCP initialization and SDK discovery metadata validation. Those integration tests do not establish real payment settlement or Bazaar indexing.

The ZIP contains the complete inputs/outputs, `cases.json`, `invalid-case.json`, `verification.json`, source-hash provenance, the HTML walkthrough, video and an unsent outreach draft. The proprietary production core is not included. The offline checker covers these fixtures; use the deployed API to evaluate new requests.

## Use the deployed capability

- [Apify Actor](https://apify.com/bono718/agent-economic-action-gate).
- [RapidAPI listing](https://rapidapi.com/bono71822/api/agent-economic-action-gate3).
- x402 request instructions are in the [capability contract](capabilities/CI-002.md#direct-api-access-x402).

This demo adds local verification; it does not repeat the earlier marketplace deployment checks. No new paid x402 purchase or wallet settlement was performed, and no claim of Bazaar search visibility is made.

## Boundaries

The caller supplies task payoff, probabilities, costs and confidence. The capability does not estimate or authenticate those values, execute agent actions or purchases, enforce a wallet budget, convert currencies or plan sequential/combined tool calls. It compares one action with independent substitutes and a zero-additional-cost baseline. Costs must be all-in and incremental; sunk costs are excluded. Actual outcomes can differ from the model.
