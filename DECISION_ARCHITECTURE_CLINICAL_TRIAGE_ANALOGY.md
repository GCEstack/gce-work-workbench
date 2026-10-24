# Evidence-First Decision Architecture — Clinical Triage Analogy

**Architecture communication case study | GCE / Edge Crew**

> **Scope warning:** This is an architectural analogy based on a sports-analytics decision framework. It is **not** a deployed or clinically validated medical device, medical diagnostic tool, clinical decision-support product, or recommendation for actual patient care. Real clinical applications would require qualified clinicians, medical governance, privacy/security controls, validation on relevant populations, regulatory analysis, and prospective safety testing. No predictive or medical effectiveness is claimed here.

## The problem this architecture addresses

Complex decisions can fail when the first plausible answer becomes the answer, source evidence is stale or conflicting, independent assessments collapse into an opaque consensus, or a polished summary hides uncertainty. Edge Crew's architecture treats the output as an **inspectable decision state** rather than a single prediction.

A hospital triage workflow is a useful explanatory analogy: before an attending clinician makes a consequential decision, data must be reconciled, independent clinical assessments kept distinguishable, uncertainty surfaced, and the original evidence preserved.

## Translation map

| Edge Crew / GCE component | Clinical workflow analogy | Architecture function |
| --- | --- | --- |
| Raw sports data and sources | Vitals, history, labs, imaging and reports | Acquire evidence with attributable origin |
| Falcon governed data substrate | Triage intake, chart/lab reconciliation | Validate identity, recency, completeness, conflicts and provenance |
| Cold analytical read | Independent clinician's first assessment | Analyze without anchoring on other interpretations |
| Warm AI | Context-informed specialist consultation | Apply explicit mandate to the evidence |
| Cold AI | Independent second opinion | Surface alternatives and overlooked failure paths |
| DATUM / SOUNDING / LATTICE | Independent quantitative risk assessments | Preserve method-specific estimates; examine divergence |
| Native scorecards | Separate consultation notes | Preserve assumptions, confidence and methodology |
| Matrix | Explicit triage-priority/weighting lens | Make decision priorities visible and comparable |
| Committee | Multidisciplinary case conference | Challenge conclusions and identify missing evidence |
| Compression | Attending summary | Reduce volume, not material uncertainty or disagreement |
| Master scorecard | Unified patient status board | Display current state and drill down to source |
| Final operating card | Decision options summary | Present actionable alternatives and supporting evidence |
| Don review and decision | Accountable human final review | Keep human decision separate from automated assessment |
| S0 outcome capture | Follow-up and retrospective quality review | Calibrate against later outcomes without altering prior records |

## Evidence rules

The input layer is *not* an expert decision-maker. It must first establish what can responsibly be claimed from the data.

- **Missing is not normal.**
- **Unavailable is not negative.**
- **Stale is not current.**
- **Proxy is not a direct measurement.**
- **Projected is not confirmed.**
- **Conflicted is not resolved.**

An interface must preserve these distinctions when rendering model outputs. An attractive dashboard that silently converts missing values to zero would violate the evidence contract.

## Independent foundations and explicit convergence

**Independent first passes:** A direct analytical read, context-aware specialist read, independent cold read, and separate quantitative methods inspect governed evidence without leaking conclusions into each other prematurely.

**Freeze native outputs:** Do not rewrite a model's original result after a subsequent reviewer challenges it. Normalize the *outer evidence envelope*—claim, sources, method, uncertainty, limitations and timestamp—without pretending different analytical methods are identical.

**Matrix:** Vary declared weighting philosophies to see where a decision changes, rather than burying priorities in one unexplained composite score.

**Committee:** Ask *what was missed?* rather than merely seeking a majority vote. New information triggers a documented reassessment, not retroactive alteration of original outputs.

**Compression:** Produce a concise operational view while preserving major disagreement, unresolved conflicts, material tail risk, and options.

**Human authority:** Present evidence for review. An override is tracked as a distinct human action, not silently backfilled into the model state.

**Outcome capture:** Compare later events with the evidence and conclusions available at decision time. Preserve the original record so hindsight does not erase uncertainty.

## Six decision lenses: illustrative analogy

| Lens | Clinical analogy | Distinct question |
| --- | --- | --- |
| 1. Price / expected value | Intervention benefit, burden and harm | What are the tradeoffs of an action? |
| 2. Traditional analytics | Observed course and longitudinal pattern | How might the situation evolve? |
| 3. Quantitative analytics | Biomarkers and measurable physiology | What does the underlying measurement suggest? |
| 4. Shape / dispersion | Instability and tail risk | What are the low-probability but high-consequence outcomes? |
| 5. Information state | Diagnostic uncertainty and evidence quality | Is the evidence sufficient for this decision? |
| 6. Don Delta | Integrative review of interacting factors | What changes when separate findings interact? |

These are **conceptual lenses**, not validated medical risk scores.

## Why this matters for AI evaluation and agentic systems

The same principles apply to coding agents and software delivery:

- A successful execution is not proof the model understood the requirement.
- Multiple agents agreeing is not proof of independent evidence.
- An agent's “saved” claim is not host-side persistence proof.
- A tool or provider failure must not be misclassified as a model reasoning failure.
- Security, correctness, performance, maintainability and domain behavior may disagree.
- Summaries must carry enough source lineage to reconstruct a critical decision.
- Human approval and post-hoc feedback must remain separately auditable.

**Core idea:** Design for a complete, traceable, uncertainty-aware decision state before any consequential action.

## Supporting portfolio evidence

- [AI evaluation case study](AI_EVALUATION_CASE_STUDY.md) — served-model identity, runtime failures and evaluation controls.
- [Coding-agent evaluation methodology](G2I_CODING_AGENT_EVALUATION_METHODOLOGY.md) — cold review, validation and structured disagreements.
- [Engineering project index](ENGINEERING_PROJECT_INDEX.md) — full-stack systems and React operator interfaces.
- [Professional portfolio](PROFESSIONAL_PORTFOLIO.md) — career overview.

This is a conceptual translation of GCE/Edge Crew methodology, not an assertion that the clinical counterpart has been built or validated.
