# Case Study — Testing the Model *as Served*, Not Just the Model Brand

**Type:** Independent AI evaluation / experimental-methodology case study  
**Evidence period:** September–October 2026  
**Sources:** GCE model test harness; frozen baseline battery; October 3–4 audition ledger and runtime/durable-state doctrine.  
**Boundary:** This is a high-level, public-safe description. It does not reproduce hidden rubrics, raw private test prompts, or confidential output artifacts.

## Problem

The same model family can behave differently when served via a different provider, adapter, runtime, tool configuration, or reasoning mode. A timeout, tool-call format mismatch, or failed save can masquerade as poor reasoning if the evaluation only records the final answer.

## Evaluation design

1. **Identify the occupant:** record model ID and version when demonstrable, provider/gateway, runtime, exposed configuration, and test battery version. Mark unknown identities explicitly.
2. **Hold the probe constant:** compare responses to a frozen test seed and predefined evaluation dimensions; preserve independent first passes where relevant.
3. **Record the behavior vector:** score objective fidelity, evidence honesty, reasoning, retrieval discipline, schema compliance, runtime reliability, and artifact persistence separately.
4. **Quarantine invalid operations:** assign operationally invalid attempts **VOID** rather than treating them as reasoning **FAIL**. Preserve observational evidence without promoting unsupported model-family conclusions.
5. **Verify state:** treat an assistant's “saved” statement as a claim until the host artifact's existence, metadata, read-back, and visibility are confirmed.
6. **Retest changes:** model updates, serving-path substitutions, and altered tool/think settings become new evaluation occupants.

## Example: Bedrock/Mantle compatibility sweep

A documented October 3 access sweep queried **50 model IDs** on one serving rail. Its recorded outcomes were **38 successful minimal executions**, **5 generic-path protocol mismatches needing retests**, and **7 access-blocked responses**.

This was an **access and protocol compatibility test**, not 50 completed quality benchmarks.

## Example: runtime failure vs model reasoning

Follow-on interactive tests recorded responses with malformed tool-call syntax and workflows diverted into irrelevant tool actions. Under the GCE method, those attempts are treated as **tool/runtime VOID**, not proof that a particular model cannot reason. In another recorded case, a file was saved only after operator intervention: the post-intervention artifact existed, but the original unattended run remained invalid for persistence compliance.

## Engineering takeaways

- A benchmark score without exact serving-path identity may not transfer between providers.
- Reproducibility requires stable probes and configuration-aware result records.
- Evaluation systems need separate dimensions for retrieval, reasoning, tool behavior, and durable output.
- Error classification is a product requirement, not just test housekeeping.

## What this case demonstrates — and does not

**Demonstrates:** a documented evaluation framework, scoped access tests, failure taxonomy, and experience auditing agent/tool behavior.

**Does not by itself demonstrate:** employment as a commercial RLHF annotator, training proprietary model weights, an externally certified benchmark, or comprehensive reasoning evaluation of every catalog-listed model.

## Source references (internal; do not publicly link without permission)

- GCE Model Test Harness README (2026-09-28).
- GCE Model Baseline/Battery Method (2026-10-03).
- GCE Model Audition Ledger (2026-10-03; updated afterward).
- GCE Model Runtime Audition and Durable State Canon (2026-10-03).
