# AI Coding-Agent Evaluation — Technical Methodology

**Candidate:** GCEstack  
**Target work:** Senior Software Engineering / AI Coding Evaluation  
**Portfolio:** [Professional portfolio](PROFESSIONAL_PORTFOLIO.md) · [Evaluation case study](AI_EVALUATION_CASE_STUDY.md) · [Engineering projects](ENGINEERING_PROJECT_INDEX.md)

## Evaluation thesis

A coding agent should be judged on more than whether its generated code passes one test. An effective assessment separates **task understanding, code correctness, execution reliability, security, evidence honesty, and the model's response to correction**. A passing happy-path test does not establish production readiness.

This framework is adapted from independent GCE multi-model testing and software engineering practice. It is a description of my approach, not a claim that G2i uses these exact procedures or that every technique below has been run against every model.

## Ten-stage review

### 1. Establish the evidence and environment
Record the observable model identity/version, provider and access path, runtime, available tools, task instructions, constraints, and prior run artifacts. Separate *unknown*, *unavailable*, *not tested*, and *negative evidence*. Do not assume an advertised tool was actually usable.

### 2. Independent cold code review
Read the implementation before the agent's explanation to reduce anchoring. Check algorithmic correctness, computational complexity, data flow, mutation, race conditions, resource handling, language idioms, testability, and security boundaries.

### 3. Compare claimed intent with implemented behavior
Read the agent's explanation and compare it with the code. Identify discrepancies, undocumented changes, questionable certainty, omitted tradeoffs, and acknowledgment of limitations. Prefer inspectable evidence over self-report.

### 4. Independent challenge
Where useful, obtain a blind second review using fresh context or another model. Preserve the reviews independently before reconciling. Agreement is not proof; disagreement is a signal for targeted investigation.

### 5. Empirical validation
Use the tests appropriate to the task: unit/integration tests, edge cases, adversarial or malformed inputs, property-based testing, fuzzing, static checks, dependency checks, benchmark/profiling, and security review. Run actual checks when execution is available; otherwise label them proposed rather than completed.

### 6. Explicit decision criteria
Define priorities for the task *before* deciding the outcome. Security, correctness, maintainability, performance, clarity, and delivery constraints differ across production systems, prototypes, and teaching examples. Do not conceal subjective priorities in a single opaque number.

### 7. Multi-lens review
Apply distinct security, performance, maintainability, and domain-correctness perspectives. Evaluate the specific failure modes each perspective contributes; do not manufacture consensus.

### 8. Preserve the result vector
Report **what works, what fails, what is uncertain, what was not tested, supporting artifacts, and the next decisive test**. Preserve disagreements across dimensions rather than averaging them away.

### 9. Synthesize cross-layer consequences
Look for issues that emerge only when evidence is combined: e.g., a passing implementation whose explanation is wrong, a correct algorithm using an unstable external API, a performant solution with a data-exposure flaw, or an apparent model failure caused by a runtime adapter.

### 10. Assign an action-oriented disposition
- **Approved within tested scope** — meets stated acceptance criteria based on observed evidence.
- **Approved with modifications** — specific remediations required before broader use.
- **Rejected** — material correctness, safety, or contract defect.
- **Needs more information** — insufficient problem constraints or unverified facts.
- **Conflicting evidence** — human review and targeted follow-up required.
- **Void / invalid run** — operational contract failed (identity, tools, access, persistence), so a reasoning verdict is not supported.

A disposition must be accompanied by evidence and scope; it is not a claim of universal reliability.

## Example failure analysis

A generated patch may compile, pass a narrow test, and describe its approach persuasively, yet call an unavailable API or violate transaction semantics. Independent cold review, contract verification, additional tests, and domain analysis expose different parts of that risk. If a coding-agent tool fails to execute, the failure should be attributed to the tool/runtime path unless model reasoning was separately observed.

## What I bring to coding-agent evaluation

- **Software judgment:** Python, TypeScript/React and API-based projects; reviewing implementations for functional and integration correctness.
- **Enterprise-domain constraints:** ERP/NetSuite operational semantics, authorization, traceability, financial data and transaction controls.
- **Hands-on AI development:** Codex, Cursor, OpenCode, Claude Code and multi-provider model workflows.
- **Evaluation discipline:** GCE baseline probes, served-configuration logging, blind comparative review, failure taxonomy, reproducibility and independent artifact verification.

[Model/provider evidence](AI_MODEL_PROVIDER_EXPERIENCE.md) includes an October 2026 **50-model-ID AWS Bedrock/Mantle access/protocol sweep**. Its 38 minimal execution successes are **not** described as 38 coding-evaluation passes.

## Relevant engineering examples

- [Runway](https://github.com/GCEstack/gce-ai-runway): Next.js/TypeScript, external integrations, Supabase, auth and code/security review artifacts.
- [Casa Companion](https://github.com/GCEstack/gce-ai-casa-companion): React/TypeScript interface, FastAPI backend and WebSocket-based voice flows.
- [Edge Crew](https://github.com/GCEstack/gce-ai-edge-crew-v3): React frontend, Python worker, database-backed workflows and multiple model integrations.

## Why the approach matters

A reliable evaluation has to answer two distinct questions: **Did the code perform the requested behavior under the observed conditions?** And **does the evidence justify trusting it in its intended environment?** The second question requires disciplined handling of unknowns, divergent reviews, failure causes, and real system constraints.

*Publication note: this document is a public-facing adaptation of the candidate-supplied G2i technical handoff. It excludes internal GCE test seeds and hidden rubrics; performance and commercial employment claims are intentionally not added without verification.*
