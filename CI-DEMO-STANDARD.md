# C.I. Factory — capability demonstration standard

For every new capability, development and deployment should include a reproducible demonstration. This standard distinguishes verified technical behavior from commercial validation.

## Required deliverables

1. A concrete problem, intended developer/user and explicit integration boundary.
2. A versioned input/output contract and complete runnable input.
3. Actual recorded implementation or API output, with execution date and provenance. Clearly distinguish local execution, mocks, marketplace requests and settled payments.
4. An independent check of the result, plus relevant edge cases and invalid-input behavior. Synthetic fixtures must be labeled; never present them as client results.
5. A small demonstration explaining the input, result and practical consequence. Include a brief video when it helps communication.
6. GitHub documentation with deployment links, usage instructions and limitations, plus an optional unsent outreach draft.
7. An audit of every public claim before promotion. A working test is not evidence of demand, real-world savings, ranking improvement or commercial adoption.

## Publishable states

- **Technical behavior demonstrated:** documented inputs, observed outputs and appropriate checks are available.
- **Delivery verified:** the relevant deployed channel has been exercised end to end. Record the exact scope; an unpaid x402 challenge or SDK metadata test does not prove settled payment or directory indexing.
- **Commercially validated:** external users have demonstrated useful adoption or purchases. Do not infer this from deployment or internal tests.

A capability can be released as an initial developer-facing version before commercial validation. Describe it according to the evidence. Follow-up work should prioritize real usage and feedback before expanding features.

## Current demonstrations

- [C.I. #01: citation remediation](CI-001-demo.md): synthetic citation scenario, original Apify output, offline before/after verification.
- [C.I. #02: economic action gate](CI-002-demo.md): synthetic estimates, actual local-core outputs, independent arithmetic verification and existing local test suite.

This document is a working convention. It does not imply that every future capability already satisfies these requirements.
