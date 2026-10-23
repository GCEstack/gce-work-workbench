# Selected Engineering Project Index

**Goal:** Make repository evidence intelligible to engineering recruiters and AI-evaluation hiring teams. The descriptions below reflect accessible repository documentation, not independently confirmed production or commercial impact.

| Codebase | Stack observed in repository docs | Engineering angle | Interview discussion |
| --- | --- | --- | --- |
| [Runway](https://github.com/GCEstack/gce-ai-runway) | Next.js, TypeScript, Supabase/Postgres, authentication, external APIs | Multi-service integrations and data model/security review | Authentication boundaries, OAuth service integration, RLS, schema migrations, critical-path bug analysis |
| [Casa Companion](https://github.com/GCEstack/gce-ai-casa-companion) | React/TypeScript PWA, Python/FastAPI, WebSockets, shared packages | Real-time voice frontend/backend architecture | Session lifecycle, streaming data, latency/reliability tradeoffs and API contract |
| [Edge Crew](https://github.com/GCEstack/gce-ai-edge-crew-v3) | React/TypeScript frontend, Python AI worker, Supabase, serverless routes | Model-processing pipeline and operator UI | Job queue behavior, model-output inspection, validation and source provenance |
| [Mission Control](https://github.com/GCEstack/mission-control) | Python/FastAPI, JavaScript dashboard, Tauri desktop, WebSockets | Developer/operator control surfaces | Local state vs UI projection, terminal routing, responsive failure recovery |

## React DevPads and operator-facing interfaces

Multiple React DevPads are part of the reported development experience. An October 4 GCE design/validation contract for the Edge Crew React DevPad describes a review UI that **must not silently alter underlying calculations**. It specifies source-to-result drilldown, provenance and uncertainty display, baseline/run comparison, and boundaries between data, math, and presentation defects.

**Evidence label:** The design requirements are documented. Full implementation and acceptance-test completion for each DevPad remain to be verified from running code and tests.

## Interview-ready engineering themes

- **Traceability:** Show how a displayed result ties back to raw source fields, transformations, and model or calculation versions.
- **State integrity:** Explain why an agent's save confirmation is weaker evidence than host-side read-back.
- **AI-generated code review:** Separate syntactic success from behavioral correctness, transaction safety, edge cases and regressions.
- **Full-stack integration:** Demonstrate the contract between React interfaces, Python or Next.js APIs, persistence, and external systems.
- **Human-in-the-loop controls:** Describe why consequential automated outputs should remain inspectable and reviewable.

## Confidentiality boundary

Potential client-related ERP project materials, named customers, internal company counts, secrets, personnel data, and unpublished GCE prompt/rubric content are **not** reproduced here. Sanitized enterprise case studies require a dedicated disclosure check before publication.
