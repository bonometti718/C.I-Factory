# C.I. #6 — worked JSON example

All figures and terms in this example are synthetic and caller supplied. Amounts are decimal strings.

## HTTP request body

```json
{
  "transaction": {
    "id": "subscription-review",
    "cash_now": "10.00",
    "terms_complete": true
  },
  "currency": {
    "code": "USD",
    "decimals": 2
  },
  "evaluation_time": "2026-10-18T12:00:00Z",
  "obligations": [
    {
      "id": "monthly-plan",
      "kind": "PAYMENT",
      "amount": "20.00",
      "frequency": "MONTH",
      "starts_at": "2026-11-01T00:00:00Z",
      "occurrences": 12,
      "minimum_commitment": "40.00",
      "cancellation": {
        "allowed_until": null
      },
      "termination_penalty": "5.00"
    }
  ]
}
```

On Apify put this object inside the `request` field.

## Actual deterministic output

```json
{
  "schema_version": "1.0",
  "capability": "ci006",
  "transaction_id": "subscription-review",
  "currency": "USD",
  "currency_decimals": 2,
  "decision": "BOUNDED",
  "cash_now": "10.00",
  "hard_committed": "45.00",
  "conditional_exposure": {
    "maximum": "0.00",
    "obligation_ids": []
  },
  "expected_exposure": "240.00",
  "maximum_exposure": "240.00",
  "recommended_reserve": "240.00",
  "cancellable_until": null,
  "next_irreversible_at": null,
  "uncapped_variables": [],
  "missing_terms": [],
  "warnings": [],
  "authorization_holds": [],
  "obligations": [
    {
      "id": "monthly-plan",
      "occurrences": 12,
      "condition": "TRUE",
      "hard_committed": "45.00",
      "maximum_exposure": "240.00",
      "expected_exposure": "240.00",
      "continuing_exposure": "240.00",
      "cancellation_cost_now": "45.00",
      "cancellable_now": true,
      "cancellable_until": null
    }
  ],
  "calculation_policy": {
    "future_only": true,
    "expected_scenario": "NO_OPTIONAL_CANCELLATION_WITH_CALLER_PROBABILITIES",
    "reserve_policy": "CONSERVATIVE_ENVELOPE_LINKED_HOLDS_NOT_DOUBLE_COUNTED",
    "recurrence_timezone": "UTC",
    "ends_at_inclusive": true,
    "rounding": "HALF_UP_TO_CURRENCY_MINOR_UNIT"
  },
  "limitations": [
    "Amounts, all-in caps, completeness and conditions are caller supplied; no natural-language contract interpretation or legal verification.",
    "Maximum exposure excludes immediate cash and authorization holds; reserve includes hold liquidity conservatively.",
    "Expected exposure is a stated scenario, not a forecast. No FX, discounting, tax inference, local-time recurrence or payment execution."
  ]
}
```

## Boundary cases

- Remove occurrences from the example: the monthly renewal is open ended. maximum_exposure and recommended_reserve become null; decision UNBOUNDED_OR_UNKNOWN. hard_committed remains 45.00 because the declared current exit costs 45.00.
- Add condition `{ "state": "UNKNOWN", "probability": "0.5" }`: decision CONDITIONAL, hard_committed 0.00, conditional maximum 240.00, expected continuing scenario 120.00.
- Set transaction.terms_complete to false: decision INSUFFICIENT_TERMS, aggregate future estimates null.
- A hold of 100.00 linked to a payment capped at 80.00 yields maximum 80.00 and reserve 100.00. The same unlinked hold yields reserve 180.00.

[Contract, calculation policy and limits](capabilities/CI-006.md).
