# GCE Model Test Case Catalogue — Public-Safe Overview

**Source of truth:** GCE Google Drive model-test harness, case-specific protocol documents and result spreadsheets.  
**Compiled:** 2026-10-23. **Scope:** Nine named numbered test cases plus the separate bootstrap preflight and related validation/registry artifacts found in a targeted Drive discovery. This is **not a complete export of all files under every Drive folder**.

> **Publication boundary:** This GitHub repository is public. This file is a sanitized catalogue only: no raw candidate prompts, unreleased hidden answers, proprietary scoring rubrics, personally sensitive case data, respondent transcripts or internal Drive URLs. The source protocols and score sheets remain in their original access-controlled Google Drive locations.

## Core test battery

| Test | Case | Primary evaluation dimensions | Status in source protocol | Protocol date |
| --- | --- | --- | --- | --- |
| 01 | Monitor selection | Search/retrieval discipline; requirements and value reasoning; resistance to generic brand recommendations | Seed defined; prompt awaiting review | 2026-09-28 |
| 02 | Phone follow-on | Authorized context carryover, personalized reasoning, preference hallucination avoidance | Dependent on Test 01; prompt awaiting review | 2026-09-28 |
| 03 | Cosmo identity | Human-intent inference grounded in researched factual context; uncertainty calibration | Seed defined; prompt awaiting review | 2026-09-28 |
| 04 | Fictional founder-intent / Disney | Blind multi-stage intent preservation, architecture and orchestration, contamination control | Case frame defined; final blind seed not frozen | 2026-09-28 |
| 05 | Outside-counsel audition | Independent gap discovery, questions, challenge behavior and bounded model-role fit | Frame defined; research seed pending | 2026-09-28 |
| 06 | Tension / ambiguity | Surfacing conflicting requirements, proposing alternatives, clarifying real tradeoffs | Behavior defined; specimen not frozen | 2026-09-28 |
| 07 | NetSuite LPN / WMS discovery | Iterative enterprise architecture, objective preservation, correction from user evidence | Case defined; prompt sequence awaiting review | 2026-10-03 |
| 08 | Objective fidelity / constraint transparency | Distinguishing provider constraints, law, capability limits, uncertainty and model judgment | Current draft; owner review pending | 2026-10-07 |
| 09 | Local edge node / network appliance | Deriving hardware and architecture from workload rather than predetermined product category | Current draft; owner review pending | 2026-10-07 |

### Prerequisite: Bootstrap preflight

Before substantive tasks, the preflight protocol checks whether a particular **model/version/provider/runtime** configuration correctly preserves assigned identity, authority boundaries, project context and session-state handling. Its review state is **ready for test design/execution** in the September 28 source.

## Evidence and corresponding source types

For cases **01–09**, Drive discovery located both:
- A named **TEST_## ... PROTOCOL** document defining the test method or draft expectations.
- A corresponding **GCE_TEST_CASE_## ...** results/working spreadsheet.

The existence of a protocol and spreadsheet **does not establish that the case was run or passed**. Consult actual dated run rows and artifacts before claiming scored results. The protocol status above reflects the source documents and may be superseded by later runs.

Additional related materials located in Drive include:
- **GCE Model Test Harness README:** test ordering, model identity, configuration logging, outcomes, and evidence/verification workflow.
- **GCE Model Test Matrix:** version/provider experience and selected trial outputs.
- **GCE Model Audition Ledger:** per-run served identities, conditions, results, tool/retrieval behavior, and Bedrock/Mantle access sweeps.
- **GCE Model Baseline / Battery Method:** frozen probes, evidence classes, repeatability and configuration-aware comparisons.
- **GCE Model Runtime Audition and Durable State Canon:** scoped FAIL vs VOID classification and persistence read-back standards.
- **GCE Don AI Validation Test Cases v1:** additional user-objective and cross-surface handoff validation scenarios.
- **Black Pearl model-labor research:** distinct analytical roles, cross-model comparison and challenge/verification.
- **Other adjacent test records:** bootstrap load testing, test publishing validation, acceptance tests and engineering-specific artifacts (indexed separately from the nine named model cases).

## How the harness evaluates models

The GCE method treats the unit of evaluation as the **served configuration**: verified model ID and version where available, provider, runtime/access path, thinking configuration, bootstrap/context and test-battery version. It distinguishes **model reasoning**, **retrieval quality**, **tool/runtime behavior**, **operational compliance**, **artifact durability** and **evidence honesty**.

A run can be **PASS**, **PARTIAL**, **FAIL** or **VOID**, with VOID used when an invalid operating contract prevents a valid reasoning verdict. Provider rate limits and tool adapter failures are not misreported as model-quality failures.

## Portfolio relevance

These cases show practical work in test design, benchmark methodology, controlled context, adversarial validation, iterative technical discovery, model-provider comparison and tool-use assessment. They are particularly relevant to **AI model evaluation**, **coding-agent evaluation**, **applied AI engineering** and **technical AI quality assurance**.

## Next verification gates (before stronger public claims)

- Reconcile every numbered case with actual runs, scores and artifact evidence; separate unrun draft protocols from executed tests.
- Compare Google Drive case spreadsheets with the model audition ledger by exact configuration and run date.
- Produce sanitized case-study write-ups for 01, 07 and 08 **only when the examples will not compromise still-active hidden assessments**.
- Confirm permissions before moving any full rubric, raw model transcript or client-specific enterprise scenario into a public repository.

**Source names preserved for internal lookup; exact Drive identifiers and private links intentionally omitted.**
