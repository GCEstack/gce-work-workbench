# GCE Model & Provider Experience Inventory — Professional Evidence Draft

**As of 2026-10-23.** Compiled from the [GCE model test matrix](https://docs.google.com/spreadsheets/d/1D75XTJntjFUogjGsvNaJrhkAzB8rb-50igt5VaJhueQ/edit), [audition ledger](https://docs.google.com/spreadsheets/d/1DXSLLZUm6bMG_2vb9fCwWDYu_dDzJ1RGi3nc5W0Hvbw/edit), [Black Pearl research anchor](https://docs.google.com/document/d/1JbEeyxTRo7xjVFr1BDmTpoRNddLWsUQDJZQWb2GekNE/edit), [model labor intelligence](https://docs.google.com/document/d/1qB3tysBCCUZ2O6UtfqdbRWJdFmre6h_3u4a2O-EZY5Q/edit), and Don's current reported use. **Internal reference for professional drafting; not a public endorsement or release of test seeds.**

## Four distinct identity layers

1. **Developer / model family:** Anthropic/Claude, Moonshot/Kimi, Z.ai/GLM, etc.
2. **Model occupant:** exact ID/version and configuration where mechanically available; operator labels are not verified underlying model identities.
3. **Serving / access provider:** AWS Bedrock Mantle, native Bedrock (access parked), OpenRouter, Azure OpenAI, Z.ai first-party, direct providers.
4. **Client / runtime / tools:** OpenCode, Codex, Cursor, Claude Code, web chat, API, DevPads.

A tool or gateway is not another independently developed model. HTTP 200 minimal inference proves only that the model ran on that path, not that it passed an engineering evaluation.

## Provider / developer family register

| Model developer or family | Documented models / versions / caveats |
|---|---|
| Moonshot AI | Kimi 2.5 Thinking, K2.8 Thinking, K3, K3 Swarm, K2.6 Hypercode/Hyperspeed, Kimi Code; separate catalog K2 Thinking |
| Z.ai | GLM 4.7, 5.1, 5.2/5.3 operator labels and first-party high-thinking observations |
| Anthropic | Claude Opus, Haiku, Claude Code access tooling; Fable label unresolved |
| OpenAI | ChatGPT, GPT-5.6 Sol operator label, Codex tooling |
| MiniMax | M2.5 live development, M2 and M2.1 observed through Mantle |
| xAI | Grok family, Grok 4.6 in Black Pearl research |
| Alibaba/Qwen | Qwen3 Coder 480B A35B, Qwen family and additional Mantle variants |
| DeepSeek | V3.1, V3.2, 3.21 operator label, Flash |
| Google | Gemini 2.5 and 3 Flash attempts; Gemma 3/4 family |
| NVIDIA | Nemotron models, exact models vary |
| Mistral | Devstral, Magistral, Ministral, Mistral Large, Voxtral through Mantle |
| Meta | Llama family, variants not pinned in source matrix |
| Cohere | North/other operator label, model identity unresolved |
| Unresolved/other | Dots3 Note Preview, Big Pickle, Space Bunny, Nex N2.5 Pro, Muse Spark 1.3, Ling 3.0 Flash, MiMo v2.6 Flash, LongCat 2.5 Preview, Apodex 1.1 Mini, Inkling Small, Fledge Alpha, Writer Palmyra Vision; do not assign developers when identity unknown |

**Current user additions, 2026-10-23:** Xiaomi (MiMo) is explicitly reported as a model family in use; the audition ledger also records `mimo-v2.6-flash-free` via OpenCode. Don additionally named **“G-R-O-K-U”**; spelling and underlying provider identity are unresolved, so do not silently equate this with Grok/xAI.

## Serving providers, rails, and tooling (not all model creators)

| Layer | Observed or reported |
|---|---|
| Serving / API / gateway | AWS Bedrock **Mantle** (distinguish from native Bedrock Runtime), OpenRouter, Azure / Azure OpenAI, Z.ai first-party/direct, direct provider APIs |
| Developer clients and runtimes | OpenCode (including free/Go paths), Codex, Cursor, Claude Code, ChatGPT/web/API, GCE React DevPads |
| Research & evaluation environments | GCE Model Audition Ledger, Test Matrix, baseline battery, Black Pearl proving ground, test harness |

## Mantle catalog and minimal execution sweep, 2026-10-03

This was a **50-ID access and protocol sweep**, **not 50 independently passed model-quality evaluations**. Recorded status is scoped to the call path and date.

| Model ID | Developer | Observed result |
|---|---|---|
| `anthropic.claude-haiku-4-5` | Anthropic | RETEST_PROTOCOL |
| `deepseek.v3.1` | DeepSeek | EXECUTION_PROVEN |
| `deepseek.v3.2` | DeepSeek | EXECUTION_PROVEN |
| `google.gemma-3-12b-it` | Google | EXECUTION_PROVEN |
| `google.gemma-3-27b-it` | Google | EXECUTION_PROVEN |
| `google.gemma-3-4b-it` | Google | EXECUTION_PROVEN |
| `google.gemma-4-26b-a4b` | Google | RETEST_PROTOCOL |
| `google.gemma-4-31b` | Google | RETEST_PROTOCOL |
| `google.gemma-4-e2b` | Google | RETEST_PROTOCOL |
| `minimax.minimax-m2` | MiniMax | EXECUTION_PROVEN |
| `minimax.minimax-m2.1` | MiniMax | EXECUTION_PROVEN |
| `minimax.minimax-m2.5` | MiniMax | EXECUTION_PROVEN |
| `mistral.devstral-2-123b` | Mistral | EXECUTION_PROVEN |
| `mistral.magistral-small-2509` | Mistral | EXECUTION_PROVEN |
| `mistral.ministral-3-14b-instruct` | Mistral | EXECUTION_PROVEN |
| `mistral.ministral-3-3b-instruct` | Mistral | EXECUTION_PROVEN |
| `mistral.ministral-3-8b-instruct` | Mistral | EXECUTION_PROVEN |
| `mistral.mistral-large-3-675b-instruct` | Mistral | EXECUTION_PROVEN |
| `mistral.voxtral-mini-3b-2507` | Mistral | EXECUTION_PROVEN |
| `mistral.voxtral-small-24b-2507` | Mistral | EXECUTION_PROVEN |
| `moonshotai.kimi-k2.5` | Moonshot AI | EXECUTION_PROVEN |
| `moonshotai.kimi-k2-thinking` | Moonshot AI | EXECUTION_PROVEN |
| `nvidia.nemotron-nano-12b-v2` | NVIDIA | EXECUTION_PROVEN |
| `nvidia.nemotron-nano-3-30b` | NVIDIA | EXECUTION_PROVEN |
| `nvidia.nemotron-nano-9b-v2` | NVIDIA | EXECUTION_PROVEN |
| `nvidia.nemotron-super-3-120b` | NVIDIA | EXECUTION_PROVEN |
| `openai.gpt-5.4` | OpenAI | ACCESS_BLOCKED_401 |
| `openai.gpt-5.4-2026-03-05` | OpenAI | ACCESS_BLOCKED_401 |
| `openai.gpt-5.5` | OpenAI | ACCESS_BLOCKED_401 |
| `openai.gpt-5.5-2026-04-23` | OpenAI | ACCESS_BLOCKED_401 |
| `openai.gpt-5.6-luna` | OpenAI | ACCESS_BLOCKED_401 |
| `openai.gpt-5.6-sol` | OpenAI | ACCESS_BLOCKED_401 |
| `openai.gpt-5.6-terra` | OpenAI | ACCESS_BLOCKED_401 |
| `openai.gpt-oss-120b` | OpenAI | EXECUTION_PROVEN |
| `openai.gpt-oss-20b` | OpenAI | EXECUTION_PROVEN |
| `openai.gpt-oss-safeguard-120b` | OpenAI | EXECUTION_PROVEN |
| `openai.gpt-oss-safeguard-20b` | OpenAI | EXECUTION_PROVEN |
| `qwen.qwen3-235b-a22b-2507` | Qwen | EXECUTION_PROVEN |
| `qwen.qwen3-32b` | Qwen | EXECUTION_PROVEN |
| `qwen.qwen3-coder-30b-a3b-instruct` | Qwen | EXECUTION_PROVEN |
| `qwen.qwen3-coder-480b-a35b-instruct` | Qwen | EXECUTION_PROVEN |
| `qwen.qwen3-coder-next` | Qwen | EXECUTION_PROVEN |
| `qwen.qwen3-next-80b-a3b-instruct` | Qwen | EXECUTION_PROVEN |
| `qwen.qwen3-vl-235b-a22b-instruct` | Qwen | EXECUTION_PROVEN |
| `writer.palmyra-vision-7b` | Writer | EXECUTION_PROVEN |
| `xai.grok-4.3` | xAI | RETEST_PROTOCOL |
| `zai.glm-4.6` | Z.AI | EXECUTION_PROVEN |
| `zai.glm-4.7` | Z.AI | EXECUTION_PROVEN |
| `zai.glm-4.7-flash` | Z.AI | EXECUTION_PROVEN |
| `zai.glm-5` | Z.AI | EXECUTION_PROVEN |

**Sweep summary reported by registry:** 38 minimal executions, 5 protocol-specific retests needed, 7 access-blocked 401 responses. Protocol failure and access denial are not model reasoning scores.

## Evaluation competence evidenced by GCE

- Version/config/path-specific model auditions; baseline batteries and regression probes.
- Distinguishes reasoning behavior, retrieval/search discipline, tool/runtime failures, identity ambiguity and artifact persistence.
- Cross-model independent comparisons, blind/contamination controls, objective fidelity and ambiguity probes.
- Capture of exact artifacts and auditable result lineage; formal VOID/FAIL separation.
- Model-assisted software design and review, React-based operator DevPads and engineering integrations.

## Publication guardrails

- Do not claim commercial RLHF engagements or employment with any model developer without evidence.
- Do not count an API catalog listing as hands-on model evaluation; classify separately.
- Do not publish confidential internal test cases, hidden rubrics or private result artifacts.
- User-reported current use is a separate evidence class from mechanically validated model identity.
- Reconcile unresolved labels (including G-R-O-K-U) before public-facing provider claims.
