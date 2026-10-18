# C.I. #5 — Worked capability substitution example

Synthetic paired fixtures. The supplied providers declare the same goal, score meaning and supported schema guarantees. The resolver does not call a sentiment model or execute either provider.

[Run on Apify](https://apify.com/bono718/agent-capability-substitution-resolver). Paste the contract into the request JSON field; HTTP accepts the contract directly.

## Input

~~~json
{
  "task_contract": {
    "goal_id": "sentiment-score/v1",
    "input_schema": {
      "type": "object",
      "properties": {
        "text": {
          "type": "string",
          "minLength": 1,
          "maxLength": 100
        }
      },
      "required": [
        "text"
      ],
      "additionalProperties": false
    },
    "output_schema": {
      "type": "object",
      "properties": {
        "score": {
          "type": "number",
          "minimum": 0,
          "maximum": 1
        }
      },
      "required": [
        "score"
      ],
      "additionalProperties": false
    },
    "output_semantics": {
      "score": "positive_sentiment_probability/v1"
    },
    "allowed_side_effects": [],
    "invariants": [
      {
        "id": "bounded-score",
        "field": "score",
        "constraint": {
          "type": "number",
          "minimum": 0,
          "maximum": 1
        }
      }
    ],
    "comparison_fields": [
      "score"
    ],
    "minimum_fixtures": 2
  },
  "incumbent_capability": {
    "id": "provider-a/v1",
    "goal_id": "sentiment-score/v1",
    "input_schema": {
      "type": "object",
      "properties": {
        "text": {
          "type": "string",
          "minLength": 1,
          "maxLength": 100
        }
      },
      "required": [
        "text"
      ],
      "additionalProperties": false
    },
    "output_schema": {
      "type": "object",
      "properties": {
        "score": {
          "type": "number",
          "minimum": 0,
          "maximum": 1
        }
      },
      "required": [
        "score"
      ],
      "additionalProperties": false
    },
    "output_semantics": {
      "score": "positive_sentiment_probability/v1"
    },
    "side_effects": []
  },
  "candidate_capability": {
    "id": "provider-b/v1",
    "goal_id": "sentiment-score/v1",
    "input_schema": {
      "type": "object",
      "properties": {
        "text": {
          "type": "string",
          "minLength": 1,
          "maxLength": 100
        }
      },
      "required": [
        "text"
      ],
      "additionalProperties": false
    },
    "output_schema": {
      "type": "object",
      "properties": {
        "score": {
          "type": "number",
          "minimum": 0,
          "maximum": 1
        }
      },
      "required": [
        "score"
      ],
      "additionalProperties": false
    },
    "output_semantics": {
      "score": "positive_sentiment_probability/v1"
    },
    "side_effects": []
  },
  "fixtures": [
    {
      "id": "positive",
      "input": {
        "text": "good"
      },
      "incumbent_output": {
        "score": 0.9
      },
      "candidate_output": {
        "score": 0.9
      },
      "incumbent_side_effects": [],
      "candidate_side_effects": []
    },
    {
      "id": "negative",
      "input": {
        "text": "bad"
      },
      "incumbent_output": {
        "score": 0.1
      },
      "candidate_output": {
        "score": 0.1
      },
      "incumbent_side_effects": [],
      "candidate_side_effects": []
    }
  ]
}
~~~

## Expected report

~~~json
{
  "schema_version": "1.0",
  "capability": "ci005",
  "decision": "DROP_IN",
  "safe_to_substitute": true,
  "assessment_scope": "DECLARED_CONTRACT_AND_SUPPLIED_FIXTURES",
  "contract_coverage": [
    {
      "field": "score",
      "source_field": "score",
      "status": "COMPATIBLE"
    }
  ],
  "compatible_fields": [
    "score"
  ],
  "behavioral_gaps": [],
  "side_effect_differences": [],
  "unknowns": [],
  "unsupported_schema_features": [],
  "fixture_results": [
    {
      "id": "negative",
      "status": "PASSED",
      "failures": [],
      "baseline_issues": []
    },
    {
      "id": "positive",
      "status": "PASSED",
      "failures": [],
      "baseline_issues": []
    }
  ],
  "adapter_spec": null,
  "required_tests": [],
  "limitations": [
    "Goal and semantic identifiers, capability guarantees and fixture executions are caller supplied and not authenticated.",
    "No tools are executed. Finite fixtures do not establish universal behavioral equivalence.",
    "safe_to_substitute applies only to the declared supported contract; it is not a production safety certification."
  ]
}
~~~

## Failure and integration cases

- Declare candidate side_effects as ["send_email"] while the task allows none: NOT_SUBSTITUTABLE. Verified in Apify cloud and direct API.
- Supply no paired fixtures: SHADOW_TEST_REQUIRED. Verified through the live direct API.
- Set candidate side_effects to null: INSUFFICIENT_EVIDENCE. Verified through the live direct API.
- Supply an explicit lossless output rename with passing evidence: ADAPTER_REQUIRED; safe_to_substitute stays false pending integration testing. Covered by local tests.
- Broaden the declared output range beyond the task guarantee: NOT_SUBSTITUTABLE, even if the two sample outputs still pass. Covered by local tests.

DROP_IN is a result under the caller-declared supported contract and supplied fixture evidence. It does not prove universal behavioral equivalence or certify production safety.

[Full scope, supported schema subset and limits](capabilities/CI-005.md).
