# C.I. #4 — Worked state conflict example

Synthetic order fixture. Stripe has payment authority over CRM; warehouse has fulfillment authority. Refunded and shipped are separate field values and can coexist unless an explicit invariant forbids that combination.

[Run on Apify](https://apify.com/bono718/agent-state-conflict-resolver). On Apify wrap this contract in `{"request": ...}`; HTTP accepts it directly.

## Input

```json
{
  "entity_id": "order-42",
  "evaluation_time": "2026-10-18T08:00:00Z",
  "sources": [
    {
      "id": "stripe"
    },
    {
      "id": "crm"
    },
    {
      "id": "warehouse"
    }
  ],
  "fields": {
    "payment": {
      "source_priority": [
        "stripe",
        "crm"
      ],
      "max_age_seconds": 3600,
      "min_confidence": 0.8,
      "require_provenance": true,
      "allowed_values": [
        "paid",
        "refunded"
      ],
      "tie_break": "ABSTAIN"
    },
    "fulfillment": {
      "source_priority": [
        "warehouse"
      ],
      "max_age_seconds": 3600,
      "min_confidence": 0.8,
      "require_provenance": true,
      "allowed_values": [
        "shipped",
        "held"
      ],
      "tie_break": "ABSTAIN"
    }
  },
  "observations": [
    {
      "id": "a",
      "entity_id": "order-42",
      "source_id": "stripe",
      "field": "payment",
      "value": "refunded",
      "observed_at": "2026-10-18T07:55:00Z",
      "confidence": 0.98,
      "provenance": "stripe:event-a"
    },
    {
      "id": "b",
      "entity_id": "order-42",
      "source_id": "crm",
      "field": "payment",
      "value": "paid",
      "observed_at": "2026-10-18T07:59:00Z",
      "confidence": 0.99,
      "provenance": "crm:event-b"
    },
    {
      "id": "c",
      "entity_id": "order-42",
      "source_id": "warehouse",
      "field": "fulfillment",
      "value": "shipped",
      "observed_at": "2026-10-18T07:58:00Z",
      "confidence": 0.95,
      "provenance": "warehouse:event-c"
    }
  ],
  "invariants": []
}

```

## Expected output

The priced Apify cloud run returned this decision contract: RESOLVED, payment refunded, fulfillment shipped, one review-only CRM patch.

```json
{
  "schema_version": "1.0",
  "capability": "ci004",
  "entity_id": "order-42",
  "decision": "RESOLVED",
  "canonical_state": {
    "fulfillment": "shipped",
    "payment": "refunded"
  },
  "candidate_state": {
    "fulfillment": "shipped",
    "payment": "refunded"
  },
  "conflicts": [
    {
      "field": "payment",
      "observations": [
        {
          "id": "a",
          "source_id": "stripe",
          "value": "refunded"
        },
        {
          "id": "b",
          "source_id": "crm",
          "value": "paid"
        }
      ]
    }
  ],
  "resolved_conflicts": [
    {
      "field": "payment",
      "rule": "SOURCE_AUTHORITY_THEN_ABSTAIN",
      "selected_observation_ids": [
        "a"
      ]
    }
  ],
  "unresolved_conflicts": [],
  "excluded_observations": [],
  "invariant_violations": [],
  "pending_invariants": [],
  "patches": [
    {
      "source_id": "crm",
      "field": "payment",
      "observed_value": "paid",
      "proposed_value": "refunded",
      "based_on_observation_id": "b",
      "requires_review": true
    }
  ],
  "provenance": {
    "fulfillment": [
      {
        "observation_id": "c",
        "source_id": "warehouse",
        "observed_at": "2026-10-18T07:58:00Z",
        "reference": "warehouse:event-c"
      }
    ],
    "payment": [
      {
        "observation_id": "a",
        "source_id": "stripe",
        "observed_at": "2026-10-18T07:55:00Z",
        "reference": "stripe:event-a"
      }
    ]
  },
  "confidence": 0.95,
  "next_safe_action": "REVIEW_PATCHES",
  "limitations": [
    "Source authority, normalization, confidence and provenance are caller supplied.",
    "No source authentication, external lookup, semantic inference or patch execution."
  ]
}
```

## Failure cases

- Add a contradictory Stripe observation without a tie-break: UNRESOLVED.
- Require refunded payment to imply held fulfillment: UNRESOLVED, invariant violation, canonical_state null and no patches.
- Remove all eligible warehouse observations: UNRESOLVED.

These cases are covered by automated core tests. No changes are applied to Stripe, CRM or warehouse systems.

[Full scope and limitations](capabilities/CI-004.md).

Additional Apify cloud check: run PfOwiMYNkFv1WPrUp returned UNRESOLVED with invariant refund-hold violated, canonical_state null, and no executable patches.
