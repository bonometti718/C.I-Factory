# Capability Infrastructure Factory

**Building machine-native infrastructure for autonomous AI agents.**

C.I. Factory is an engineering project focused on identifying emerging infrastructure gaps in agentic systems and turning them into small, deterministic, verifiable capabilities.

The objective is not to build another general-purpose agent. It is to build the infrastructure autonomous agents need around execution: verification, economic control, state consistency, remediation, and other machine-native primitives.

## Capability Portfolio

| C.I. | Capability | Status |
|---|---|---|
| #01 | [Citation Remediation Payload Generator](capabilities/CI-001.md) | [LIVE · Apify](https://apify.com/bono718/citation-remediation-payload-generator) |
| #02 | [Agent Economic Action Gate](capabilities/CI-002.md) | [LIVE · Apify](https://apify.com/bono718/agent-economic-action-gate) · [LIVE · Railway](https://ci-002-production.up.railway.app/health) · [LIVE · RapidAPI](https://rapidapi.com/bono71822/api/agent-economic-action-gate3) |

> The public portfolio lists only capabilities that have been deployed. New C.I.s are added here after deployment is verified.

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
