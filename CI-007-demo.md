# C.I. #7 — invariant coverage gap demo

This synthetic graph and its witness references are caller-supplied examples. The API does not execute these tests or authenticate their outcomes.

## Request body

```json
{
  "graph": {
    "nodes": [
      {
        "id": "planner",
        "type": "agent"
      },
      {
        "id": "worker",
        "type": "agent"
      },
      {
        "id": "payment",
        "type": "effect"
      }
    ],
    "edges": [
      {
        "from": "planner",
        "to": "payment",
        "mode": "DIRECT"
      },
      {
        "from": "planner",
        "to": "worker",
        "mode": "DELEGATED"
      },
      {
        "from": "worker",
        "to": "payment",
        "mode": "DIRECT"
      },
      {
        "from": "planner",
        "to": "payment",
        "mode": "RETRY"
      }
    ]
  },
  "invariants": [
    {
      "id": "spend-cap",
      "effect": "payment",
      "operator": "BOUND",
      "field": "amount",
      "comparison": "<=",
      "value": 100,
      "scope": "cumulative"
    }
  ],
  "evidence": [
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DIRECT",
      "condition": "ABOVE_THRESHOLD",
      "result": "PASS",
      "witness_id": "test:DIRECT:ABOVE_THRESHOLD"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DELEGATED",
      "condition": "AT_THRESHOLD",
      "result": "PASS",
      "witness_id": "test:DELEGATED:AT_THRESHOLD"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DIRECT",
      "condition": "AT_THRESHOLD",
      "result": "PASS",
      "witness_id": "test:DIRECT:AT_THRESHOLD"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "AT_THRESHOLD",
      "result": "PASS",
      "witness_id": "test:RETRY:AT_THRESHOLD"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DELEGATED",
      "condition": "BELOW_THRESHOLD",
      "result": "PASS",
      "witness_id": "test:DELEGATED:BELOW_THRESHOLD"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DIRECT",
      "condition": "BELOW_THRESHOLD",
      "result": "PASS",
      "witness_id": "test:DIRECT:BELOW_THRESHOLD"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "BELOW_THRESHOLD",
      "result": "PASS",
      "witness_id": "test:RETRY:BELOW_THRESHOLD"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "MULTI_ACTION_BELOW",
      "result": "PASS",
      "witness_id": "test:RETRY:MULTI_ACTION_BELOW"
    }
  ]
}
```

On Apify wrap the object in the `request` field. HTTP takes it directly.

## Actual output

```json
{
  "schema_version": "1.0",
  "capability": "ci007",
  "coverage_model": "ci007-dag-v1",
  "status": "GAPS_FOUND",
  "coverage": {
    "required": 12,
    "covered": 8,
    "uncovered": 4,
    "conflicting": 0,
    "ratio": 0.6667
  },
  "entrypoints": [
    "planner"
  ],
  "invariants": [
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "normalized_invariant": {
        "id": "spend-cap",
        "effect": "payment",
        "operator": "BOUND",
        "field": "amount",
        "comparison": "<=",
        "value": 100,
        "scope": "cumulative"
      },
      "coverage": {
        "required": 12,
        "covered": 8,
        "uncovered": 4,
        "conflicting": 0,
        "ratio": 0.6667
      },
      "status": "GAPS_FOUND"
    }
  ],
  "obligations": [
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DELEGATED",
      "condition": "ABOVE_THRESHOLD",
      "expected_case": "VIOLATES",
      "status": "UNCOVERED",
      "passing_witnesses": [],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DIRECT",
      "condition": "ABOVE_THRESHOLD",
      "expected_case": "VIOLATES",
      "status": "COVERED",
      "passing_witnesses": [
        "test:DIRECT:ABOVE_THRESHOLD"
      ],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "ABOVE_THRESHOLD",
      "expected_case": "VIOLATES",
      "status": "UNCOVERED",
      "passing_witnesses": [],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DELEGATED",
      "condition": "AT_THRESHOLD",
      "expected_case": "SATISFIES",
      "status": "COVERED",
      "passing_witnesses": [
        "test:DELEGATED:AT_THRESHOLD"
      ],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DIRECT",
      "condition": "AT_THRESHOLD",
      "expected_case": "SATISFIES",
      "status": "COVERED",
      "passing_witnesses": [
        "test:DIRECT:AT_THRESHOLD"
      ],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "AT_THRESHOLD",
      "expected_case": "SATISFIES",
      "status": "COVERED",
      "passing_witnesses": [
        "test:RETRY:AT_THRESHOLD"
      ],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DELEGATED",
      "condition": "BELOW_THRESHOLD",
      "expected_case": "SATISFIES",
      "status": "COVERED",
      "passing_witnesses": [
        "test:DELEGATED:BELOW_THRESHOLD"
      ],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DIRECT",
      "condition": "BELOW_THRESHOLD",
      "expected_case": "SATISFIES",
      "status": "COVERED",
      "passing_witnesses": [
        "test:DIRECT:BELOW_THRESHOLD"
      ],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "BELOW_THRESHOLD",
      "expected_case": "SATISFIES",
      "status": "COVERED",
      "passing_witnesses": [
        "test:RETRY:BELOW_THRESHOLD"
      ],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "MULTI_ACTION_ABOVE",
      "expected_case": "VIOLATES",
      "status": "UNCOVERED",
      "passing_witnesses": [],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "MULTI_ACTION_AT",
      "expected_case": "SATISFIES",
      "status": "UNCOVERED",
      "passing_witnesses": [],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "MULTI_ACTION_BELOW",
      "expected_case": "SATISFIES",
      "status": "COVERED",
      "passing_witnesses": [
        "test:RETRY:MULTI_ACTION_BELOW"
      ],
      "failing_witnesses": []
    }
  ],
  "uncovered_obligations": [
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DELEGATED",
      "condition": "ABOVE_THRESHOLD",
      "expected_case": "VIOLATES",
      "status": "UNCOVERED",
      "passing_witnesses": [],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "ABOVE_THRESHOLD",
      "expected_case": "VIOLATES",
      "status": "UNCOVERED",
      "passing_witnesses": [],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "MULTI_ACTION_ABOVE",
      "expected_case": "VIOLATES",
      "status": "UNCOVERED",
      "passing_witnesses": [],
      "failing_witnesses": []
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "RETRY",
      "condition": "MULTI_ACTION_AT",
      "expected_case": "SATISFIES",
      "status": "UNCOVERED",
      "passing_witnesses": [],
      "failing_witnesses": []
    }
  ],
  "unreachable_obligations": [
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DELEGATED",
      "condition": "MULTI_ACTION_ABOVE",
      "expected_case": "VIOLATES",
      "reason": "MULTI_ACTION_NOT_DECLARED"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DIRECT",
      "condition": "MULTI_ACTION_ABOVE",
      "expected_case": "VIOLATES",
      "reason": "MULTI_ACTION_NOT_DECLARED"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DELEGATED",
      "condition": "MULTI_ACTION_AT",
      "expected_case": "SATISFIES",
      "reason": "MULTI_ACTION_NOT_DECLARED"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DIRECT",
      "condition": "MULTI_ACTION_AT",
      "expected_case": "SATISFIES",
      "reason": "MULTI_ACTION_NOT_DECLARED"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DELEGATED",
      "condition": "MULTI_ACTION_BELOW",
      "expected_case": "SATISFIES",
      "reason": "MULTI_ACTION_NOT_DECLARED"
    },
    {
      "invariant_id": "spend-cap",
      "invariant_signature": "4d428aeec56889ddb78341d9c252df15e60131af38ce8c393bea6a30ef4a9606",
      "surface": "payment",
      "mode": "DIRECT",
      "condition": "MULTI_ACTION_BELOW",
      "expected_case": "SATISFIES",
      "reason": "MULTI_ACTION_NOT_DECLARED"
    }
  ],
  "conflicting_evidence": [],
  "stale_evidence": [],
  "coverage_policy": {
    "graph": "DAG_ALLOWED_ROOT_TO_LEAF_TRANSITIONS",
    "mode": "PREFIX_RETRY_THEN_DELEGATED_ELSE_DIRECT",
    "sequence": "A_BEFORE_B_B_BEFORE_A_B_ONLY_ON_COMPLETE_TRACES_WITH_B",
    "multi_action": "CUMULATIVE_BOUND_ONLY_RETRY_OR_EFFECT_REPEATABLE",
    "evidence": "PASS_MEANS_VERIFICATION_CHECK_PASSED_INCLUDING_EXPECTED_REJECTION",
    "ratio": "COVERED_DIVIDED_BY_REQUIRED_NULL_WHEN_NO_REQUIRED"
  },
  "limitations": [
    "Coverage is relative to the caller-declared graph, invariants, repeatability and evidence; not a proof of correctness or safety.",
    "Witnesses and results are not executed, authenticated or semantically evaluated. No tests are generated.",
    "Retry is an abstract mode, not an unrolled cycle. Combined modes, concurrency, data-dependent feasibility and cross-invariant constraints are not modeled.",
    "Boundary cases describe real-number relations for BOUND, scalar membership, nonnegative integer cardinality and graph ordering. They do not synthesize concrete test inputs."
  ]
}
```

## Mutation checks

- Remove a PASS evidence record: the corresponding covered obligation becomes uncovered.
- Fill the four missing obligations with current-signature PASS evidence: COVERED, 12 required, 12 covered, ratio 1. This is coverage under the declared model, not safety certification.
- Add FAIL evidence to a currently passing obligation: CONFLICTING_EVIDENCE; the obligation no longer counts as covered.
- Change the bound from 100 to 99 and keep the eight old evidence records: all eight are stale, none covers the new invariant; 12 gaps remain.
- Remove all graph edges and submit no evidence: NO_REACHABLE_OBLIGATIONS, required 0, ratio null. Evidence for newly unreachable obligations must be removed or returns EVIDENCE_WITHOUT_OBLIGATION.

[Full contract, semantics and limits](capabilities/CI-007.md).
