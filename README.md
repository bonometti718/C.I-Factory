# C.I. FACTORY — Capability Infrastructure Factory

**From missing digital capabilities to small, deployable software components.**

C.I. FACTORY is an independent software capability factory. We look for specific infrastructure gaps in existing and emerging digital ecosystems, define the smallest useful capability that fills each gap, and build reusable components with explicit interfaces and verifiable behavior.

**The Factory is not a single Actor, API, or AI product.** It is the engineering process and growing portfolio behind independently usable capabilities. Our first deployments focus on AI search and agent infrastructure, but the model also applies to developer tools, automation, social platforms, data workflows, and future ecosystems.

[Explore the capability catalog](#capability-catalog) · [How we work](#how-the-factory-works) · [Integration](#integrate-a-capability) · [Contact](#contact)

## How the Factory works

1. **Scout:** identify an underserved, concrete software need.
2. **Define:** specify one narrow machine-readable input/output contract and clear limits.
3. **Build:** implement a lightweight, low-marginal-cost capability.
4. **Verify:** test supported cases, edge cases and failure modes with reproducible examples.
5. **Distribute:** publish suitable integrations through Actors, APIs or developer marketplaces.
6. **Iterate:** prioritize improvements based on real integration feedback and adoption.

The goal is not to accumulate features or listings for their own sake. Each capability must solve a distinct problem and be independently useful to developers and integrators.

## Capability catalog

The repository currently documents **seven deployed capabilities**. Each has its own technical documentation; marketplace and API links are listed separately below.

| C.I. | Capability | Distribution |
| --- | --- | --- |
| #01 | [Citation Remediation Payload Generator](capabilities/CI-001.md) | [Apify](https://apify.com/bono718/citation-remediation-payload-generator) |
| #02 | [Agent Economic Action Gate](capabilities/CI-002.md) | [Apify](https://apify.com/bono718/agent-economic-action-gate) · [RapidAPI](https://rapidapi.com/bono71822/api/agent-economic-action-gate3) · [x402](https://ci-002-production.up.railway.app/x402/v1/evaluate) |
| #03 | [Agent Evidence Sufficiency Engine](capabilities/CI-003.md) | [Apify](https://apify.com/bono718/agent-evidence-sufficiency-engine) · [RapidAPI](https://rapidapi.com/bono71822/api/agent-evidence-sufficiency-engine) · [x402](https://ci-002-production.up.railway.app/ci003/x402/v1/evaluate) |
| #04 | [Agent State Conflict Resolver](capabilities/CI-004.md) | [Apify](https://apify.com/bono718/agent-state-conflict-resolver) · [RapidAPI](https://rapidapi.com/bono71822/api/agent-state-conflict-resolver) · [x402](https://ci-002-production.up.railway.app/ci004/x402/v1/evaluate) |
| #05 | [Agent Capability Substitution Resolver](capabilities/CI-005.md) | [Apify](https://apify.com/bono718/agent-capability-substitution-resolver) · [RapidAPI](https://rapidapi.com/bono71822/api/agent-capability-substitution-resolver) · [x402](https://ci-002-production.up.railway.app/ci005/x402/v1/evaluate) |
| #06 | [Agent Future Obligation Exposure Resolver](capabilities/CI-006.md) | [Apify](https://apify.com/bono718/agent-future-obligation-exposure-resolver) · [RapidAPI](https://rapidapi.com/bono71822/api/agent-future-obligation-exposure-resolver) · [x402](https://ci-002-production.up.railway.app/ci006/x402/v1/evaluate) |
| #07 | [Agent Invariant Coverage Gap Resolver](capabilities/CI-007.md) | [Apify](https://apify.com/bono718/agent-invariant-coverage-gap-resolver) · [RapidAPI](https://rapidapi.com/bono71822/api/agent-invariant-coverage-gap-resolver) · [x402](https://ci-002-production.up.railway.app/ci007/x402/v1/evaluate) |

> **Distribution note:** Links reflect published integrations documented in this repository. Different channels may have different access requirements, pricing and endpoint semantics. Publication does not establish usage, customer demand or revenue. New capabilities are added to this public catalog after their deployment has been verified.

## What each capability does

### C.I. #01 — Citation Remediation Payload Generator

**Problem:** an AI answer cites another website and overlooks a relevant target page even when the supplied HTML contains usable facts.

Given citation evidence, target and competitor HTML snapshots, and grounded facts, this component produces deterministic remediation instructions: proposed HTML additions, WebPage JSON-LD, snapshot checks and typed acceptance tests. An external adapter reviews and applies changes. It does **not** collect live citations or guarantee better search visibility.

[Input schema, example and Apify quickstart](capabilities/CI-001.md) · [Worked demo](CI-001-demo.md)

### C.I. #02 — Agent Economic Action Gate

**Problem:** an agent needs to decide whether to pay for a tool call or verification action rather than use a baseline or substitute.

Compares caller-supplied expected values and costs, returning a deterministic `BUY`, `SKIP`, `STOP` or `ESCALATE` result, a modeled advantage and a maximum rational price. It does **not** execute purchases or estimate unknown success probabilities.

A documented example evaluates a USD 3 verifier and returns `BUY`, a USD 7 rational price ceiling and USD 4 modeled advantage over the best alternative.

[Contract and Apify/RapidAPI/x402 examples](capabilities/CI-002.md) · [Worked demo](CI-002-demo.md)

### C.I. #03 — Agent Evidence Sufficiency Engine

**Problem:** a structured claim needs to meet evidence requirements before an automated workflow treats it as supported.

Checks declared source count, source type, freshness, provenance references and confidence requirements; reports `SUPPORTED`, `CONTRADICTED` or `INSUFFICIENT` with traceable reasons. It uses exact JSON-value comparison, **not** semantic fact-checking or independent source authentication.

[Technical documentation](capabilities/CI-003.md) · [Worked JSON demo](CI-003-demo.md)

### C.I. #04 — Agent State Conflict Resolver

**Problem:** connected systems report incompatible values for the same entity.

Applies explicit field-level source authority, freshness and invariants to return a canonical state or escalate unresolved conflicts. Any proposed changes are review-only: the component does **not** write to external systems.

[Technical documentation](capabilities/CI-004.md) · [Conflict demo and failure cases](CI-004-demo.md)

### C.I. #05 — Agent Capability Substitution Resolver

**Problem:** a replacement API can look similar to an existing one without satisfying the same task contract.

Compares declared schema guarantees, semantic identifiers, permitted effects and paired fixtures. Reports direct substitution, adapter work, required tests, insufficient evidence or incompatibility. It does **not** claim broader equivalence than the provided contract and evidence support.

[Technical documentation](capabilities/CI-005.md) · [Substitution demo and failure cases](CI-005-demo.md)

### C.I. #06 — Agent Future Obligation Exposure Resolver

**Problem:** a small immediate charge can hide future renewals, deferred fees, cancellation penalties or liquidity commitments.

Separates cash due now, unavoidable commitments, conditional liability, expected continuation scenarios, maximum future exposure and conservative reserves. Unknown or uncapped amounts remain unknown. It uses structured terms and does **not** interpret legal contracts or make payments.

[Technical documentation](capabilities/CI-006.md) · [Liability demo and boundary cases](CI-006-demo.md)

### C.I. #07 — Agent Invariant Coverage Gap Resolver

**Problem:** passing a direct-path test does not prove that delegated, retry or cumulative execution paths have been verified.

Projects structured invariants onto reachable execution paths, matches compatible evidence and reports covered, missing, unreachable and conflicting verification obligations. It does **not** generate or execute tests or certify that an agent is safe.

[Technical documentation](capabilities/CI-007.md) · [Coverage demo and mutation cases](CI-007-demo.md)

## Integrate a capability

**Start with the capability-specific documentation**, not the whole Factory. Each technical page explains the component's purpose, input/output contract, supported behavior, examples, limitations and available distribution channels.

- **Apify:** access the published Actors from the catalog links.
- **RapidAPI:** open each listed API page for its request format and platform access details.
- **x402:** invoke the listed payment-enabled JSON API endpoints with an appropriate client. Opening an endpoint in a browser sends a `GET` request and does not perform a paid evaluation. A valid unpaid `POST` may return HTTP `402 Payment Required`; see the relevant capability documentation for supported request and payment flows.
- **Railway:** the [gateway health endpoint](https://ci-002-production.up.railway.app/health) is a health check, not a capability evaluation.

**Pricing and availability can change by channel**; refer to marketplace listings and API documentation for current terms.

## Engineering principles

- **Small, independent capabilities** with a clearly defined responsibility.
- **Machine-native, versioned contracts** instead of ambiguous inputs and outputs.
- **Deterministic behavior where feasible**, with reproducible verification.
- **Low marginal execution costs** and limited unnecessary dependencies.
- **Portable core logic**, separated from distribution-specific adapters.
- **Explicit limits and failure modes**, without unsupported claims of autonomy, correctness or commercial traction.

## Contact

For integrations, technical questions or commercial inquiries: [bonometti.work.AI@gmail.com](mailto:bonometti.work.AI@gmail.com).

---

**C.I. FACTORY** · Independent software capabilities for emerging digital ecosystems.
