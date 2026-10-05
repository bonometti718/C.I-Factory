# C.I. #01 — AI citation remediation: reproducible demo

An AI answer cites a competitor and omits Acme, even though Acme's supplied page says it exports CSV. C.I. #01 returns an explicit HTML/JSON-LD change plan that a consumer can review, apply and verify.

**Fictional scenario, real Actor output.** Acme, the URLs, the AI answer and citation evidence are simulated fixtures. The output is an original export from a successful Apify run on 1 October 2026, retrieved on 5 October. This is a replay of that run, not a newly purchased execution or evidence of improved AI citations.

## See the result

- [Download the complete demo](CI-001-demo.zip), extract it and open `CI-001-demo/demo.html`.
- Watch `walkthrough.mp4`: a 60-second walkthrough of the fixture and observed output, not a screen recording of a new run.
- Run `python verify.py` inside the extracted folder (Python 3, no dependencies).
- [Run the Actor on Apify](https://apify.com/bono718/citation-remediation-payload-generator).
- [Full capability contract and API quickstart](capabilities/CI-001.md).

## Before → after

Before: `<h1>Acme</h1>` and a paragraph confirming CSV exports. No heading answering the query and no WebPage JSON-LD.

The observed `ready` payload proposes two additions:

```html
<section id="cr-31e479b6c08a"><h2>Does Acme export CSV?</h2><p>Acme exports reports in CSV format.</p></section>
```

```json
{"@context":"https://schema.org","@type":"WebPage","@id":"https://example.com/product#webpage","url":"https://example.com/product"}
```

The offline consumer applies both additions to `body`. All three supplied acceptance tests fail before and pass after: section count, grounded text in that section and WebPage URL. Target/competitor snapshot hashes and answer hash match. Altered snapshots and already-recorded change IDs are rejected.

## Reproducibility and boundaries

The ZIP contains `input.json`, the original `output.json`, `before.html`, `after.html`, `competitor.html`, `verify.py`, `verification.json`, `applied-change-ids.json` and `provenance.json`.

Actor ID: `Ex2lIxIRmW5LggKfM`. Run ID: `BXghcwQxiNXqZN5uF`. Dataset ID: `ZcB59X07P6LSs70ja`. Console: succeeded, one result, four seconds.

`verify.py` is a deliberately narrow consumer for this fixture, not a production CMS integration or the Actor's proprietary core. It supports `body` and ID selectors and checks all preconditions against the original snapshot before writing. Review and sanitize supplied HTML before production use; keep rollback data and a persistent change-ID ledger. The Actor's whole-input hash is preserved but not recomputed here because its canonicalization algorithm is outside this example.

The Actor does not fetch current pages, observe live AI citations, edit your CMS, or guarantee citation uplift. This demo proves the change-plan and local verification workflow. It does not prove that an AI engine will cite Acme afterwards.
