# Capability Infrastructure Factory

**Deterministic tools for AI citation remediation and autonomous agent decisions.**

Turn supplied AI citation evidence into HTML and JSON-LD remediation plans, or evaluate whether an agent action is worth its cost. Explore the live capabilities below and run them through their marketplace APIs.

C.I. Factory is an engineering project focused on identifying emerging infrastructure gaps in agentic systems and turning them into small, deterministic, verifiable capabilities.

The objective is not to build another general-purpose agent. It is to build the infrastructure autonomous agents need around execution: verification, economic control, state consistency, remediation, and other machine-native primitives.

## Capability Portfolio

| C.I. | Capability | Status |
|---|---|---|
| #01 | [Citation Remediation Payload Generator](capabilities/CI-001.md) | [LIVE · Apify](https://apify.com/bono718/citation-remediation-payload-generator) |
| #02 | [Agent Economic Action Gate](capabilities/CI-002.md) | [LIVE · Apify](https://apify.com/bono718/agent-economic-action-gate) · [LIVE · Railway](https://ci-002-production.up.railway.app/health) · [LIVE · RapidAPI](https://rapidapi.com/bono71822/api/agent-economic-action-gate3) |

> The public portfolio lists only capabilities that have been deployed. New C.I.s are added here after deployment is verified.

## Fix an AI citation gap with C.I. #01

**Problem:** an AI answer cites a competitor and omits your page, while the relevant facts already exist in your HTML.

[**Citation Remediation Payload Generator — run on Apify**](https://apify.com/bono718/citation-remediation-payload-generator) turns supplied citation evidence, target and competitor HTML snapshots, and grounded facts into deterministic remediation instructions. Outputs include proposed HTML additions, WebPage JSON-LD, snapshot checks, and typed acceptance tests. Your own adapter reviews and applies the changes.

Useful for generative engine optimization (GEO), answer engine optimization (AEO), AI search visibility, and agent-driven content maintenance workflows that already collect citation evidence. It does not collect live citations or guarantee citation uplift.

[**Start here: complete JSON input, Apify quickstart, and cURL API example**](capabilities/CI-001.md). One target page, one competitor, and one query per run.

## Decide whether an agent should pay with C.I. #02

**Problem:** an agent can buy a tool call or verification step, but must compare its expected benefit with its price, baseline, and available substitutes.

[**Agent Economic Action Gate**](capabilities/CI-002.md) provides deterministic expected-value comparison, a `BUY` / `SKIP` / `STOP` / `ESCALATE` decision, and a maximum rational price from caller-supplied estimates. Useful for AI agent cost control, tool-call economics, and paid capability selection. It does not execute purchases or estimate success probabilities.

**Verified example:** a USD 3 verifier returns `BUY`, a USD 7 price ceiling, and USD 4 modeled advantage over the best substitute. [Complete JSON input and API quickstarts for Apify, RapidAPI, and x402](capabilities/CI-002.md).

## Use C.I. #02 via x402

**[Agent Economic Action Gate - paid API endpoint](https://ci-002-production.up.railway.app/x402/v1/evaluate)**

Send a JSON `POST` request to evaluate whether an agent should buy an action versus its baseline and alternatives. Price: **0.001 USDC per evaluation on Base mainnet**. An unpaid valid request returns `402 Payment Required`; an x402-compatible client can sign the payment authorization and retry to receive the result.

Opening the link in a browser sends GET and does not run an evaluation. See the [request example and usage instructions](capabilities/CI-002.md#direct-api-access-x402).

## Use C.I. #02 via RapidAPI

[Open Agent Economic Action Gate on RapidAPI](https://rapidapi.com/bono71822/api/agent-economic-action-gate3). Send JSON to `POST /rapidapi/v1/evaluate` using your RapidAPI application key. **Pay per use: $0.002 per request, with no monthly subscription fee.** RapidAPI platform bandwidth fees may also apply.

The gateway integration was tested successfully: HTTP `200 OK`, decision `BUY`, and `max_rational_price: 7` for the documented example. See the [capability documentation](capabilities/CI-002.md) for inputs and operational boundaries.

## Design Principles

- Machine-native inputs and outputs
- Deterministic behavior wherever possible
- Automatically verifiable results
- Low marginal execution cost
- Marketplace-agnostic core
- Thin adapters for deployment surfaces
- Versioned contracts and reproducible tests

## What We Build

C.I. Factory targets missing infrastructure between autonomous agents and reliable real-world execution: small, machine-native capabilities with explicit contracts and verifiable outputs.

## Explore the Live Capabilities

Start with the two deployed capabilities above. Each public capability page documents its purpose, machine contract, example input, operational boundaries, and deployment status.

Both deployed capabilities can be opened and run directly on Apify from the links above. C.I. #02 is also available through RapidAPI and the direct x402 endpoint.

---

**C.I. Factory** · Capability Infrastructure for autonomous systems


## Contact

For integration questions and feedback: [bonometti.work.AI@gmail.com](mailto:bonometti.work.AI@gmail.com).
