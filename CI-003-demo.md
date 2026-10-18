# C.I. #3 — Worked evidence-contract example

Verified on Apify on 18 October 2026, build 0.1.2. This is a synthetic shipment fixture, not evidence of a real delivery.

## Run the tool

[Open Actor on Apify](https://apify.com/bono718/agent-evidence-sufficiency-engine). Paste the following JSON in the input editor and start. An Apify account is required. Price: $0.002 per verdict plus $0.00005 startup at 256 MB.

```json
{
  "mode": "outcome",
  "claim_or_condition": {
    "id": "shipment_delivered",
    "expected_value": true
  },
  "evaluation_time": "2026-10-18T07:00:00Z",
  "evidence_requirements": {
    "minimum_independent_sources": 2,
    "required_source_types": [
      "carrier",
      "receiver"
    ],
    "max_age_seconds": 86400,
    "confidence_threshold": 0.8,
    "require_provenance": true
  },
  "evidence_bundle": [
    {
      "id": "carrier-a-event",
      "claim_id": "shipment_delivered",
      "source_id": "carrier-a",
      "source_type": "carrier",
      "independence_group": "carrier-a",
      "observed_at": "2026-10-18T06:00:00Z",
      "provenance": {
        "reference": "carrier-a:record:123"
      },
      "confidence": 0.95,
      "value": true
    },
    {
      "id": "receiver-b-event",
      "claim_id": "shipment_delivered",
      "source_id": "receiver-b",
      "source_type": "receiver",
      "independence_group": "receiver-b",
      "observed_at": "2026-10-18T06:30:00Z",
      "provenance": {
        "reference": "receiver-b:record:123"
      },
      "confidence": 0.9,
      "value": true
    }
  ]
}
```

## Expected result

SUPPORTED, two independent groups, carrier and receiver present, minimum caller confidence 0.9. The complete local expected output is below; the priced cloud run returned the same decision contract.

```json
{
  "schema_version": "1.0",
  "policy_version": "ci003-exact-value-v1",
  "mode": "outcome",
  "claim_id": "shipment_delivered",
  "evaluation_time": "2026-10-18T07:00:00Z",
  "decision": "SUPPORTED",
  "confidence": 0.9,
  "confidence_basis": "MINIMUM_CALLER_SUPPLIED_CONFIDENCE; NOT_CALIBRATED_TRUTH_PROBABILITY",
  "supporting_evidence_ids": [
    "carrier-a-event",
    "receiver-b-event"
  ],
  "contradicting_evidence_ids": [],
  "satisfied_requirements": [
    "SUPPORTING_EVIDENCE_CONTRACT"
  ],
  "missing_requirements": [],
  "independence_assessment": {
    "basis": "CALLER_DECLARED_GROUPS_OR_SOURCE_IDS; NOT_INDEPENDENTLY_VERIFIED",
    "supporting": 2,
    "contradicting": 0
  },
  "freshness_assessment": {
    "stale_evidence_ids": [],
    "future_evidence_ids": []
  },
  "provenance_assessment": {
    "basis": "REFERENCE_PRESENCE_ONLY; NOT_AUTHENTICATED",
    "missing_evidence_ids": []
  },
  "reason_codes": [
    "SUPPORT_CONTRACT_MET"
  ],
  "resolution_details": {
    "policy": "insufficient_on_conflict",
    "comparison": "EXACT_JSON_VALUE",
    "conflict": false,
    "evidence_assessments": [
      {
        "evidence_id": "carrier-a-event",
        "source_id": "carrier-a",
        "source_type": "carrier",
        "independence_group": "carrier-a",
        "age_seconds": 3600,
        "eligible": true,
        "reasons": [],
        "relation": "SUPPORT",
        "confidence": 0.95
      },
      {
        "evidence_id": "receiver-b-event",
        "source_id": "receiver-b",
        "source_type": "receiver",
        "independence_group": "receiver-b",
        "age_seconds": 1800,
        "eligible": true,
        "reasons": [],
        "relation": "SUPPORT",
        "confidence": 0.9
      }
    ],
    "support_contract": {
      "independent_source_count": 2,
      "missing": [],
      "meets_requirements": true
    },
    "contradiction_contract": {
      "independent_source_count": 0,
      "missing": [
        "MINIMUM_INDEPENDENT_SOURCES",
        "REQUIRED_SOURCE_TYPE:carrier",
        "REQUIRED_SOURCE_TYPE:receiver"
      ],
      "meets_requirements": false
    }
  }
}

```

## Try the failure cases

- Remove the receiver record: INSUFFICIENT; missing independent source and receiver type. Verified in a separate cloud run.
- Change receiver value to false: INSUFFICIENT under the default conflict policy. Covered by local tests.
- Change both values to false: CONTRADICTED. Covered by local tests.
- Give both records the same independence_group: INSUFFICIENT. Covered by local tests.

21 local automated tests pass. Cloud build 0.1.2 SUCCEEDED; priced run EFYQ6CVpWc0iGtDhh SUCCEEDED, dataset YXJ787ijfja7XmQmo, event counts: one apify-actor-start and one apify-default-dataset-item. Owner testing verifies event accounting, not third-party revenue.

## Boundaries

Strict JSON equality only. Caller normalizes evidence and declares source groups and confidence. The tool does not determine real-world truth, read prose semantically, prove independence or authenticate provenance. Evaluation time is explicit and fixed for reproducibility.

[Full capability](capabilities/CI-003.md)
