# Invocation Framework — Integration Specification

This document defines how the Invocation Framework integrates with three categories of AI systems: OpenAI models, Anthropic models, and local LLMs. The purpose is to ensure that all AI agents—regardless of vendor—produce consistent, deterministic, machine-verifiable Invocation outputs using the same schemas, governance standards, and decision architecture.

The Invocation Framework consists of shared machine schemas, a unified decision-pathway model, structured-content rules, and a formal Invocation Protocol. All integrations MUST conform to these specifications for consistency.

---

# 1. OpenAI Integration (GPT-4.1, GPT-5, o-series)

OpenAI models use a function-first, schema-guided workflow. This maps cleanly to Invocation Architecture.

## Required Components
OpenAI integrations must import:

- `invocation-entity-schema.json`
- `invocation-decision-pathway-schema.json`
- `invocation-signal-schema.json`
- `product-schema.json` and/or `service-schema.json`
- `invocation-protocol-v0.1.md`

These define valid entities, signals, constraints, scoring strategies, and required output fields.

## Execution Flow
1. **Intent Parsing**  
   Detect domain, intent type, and user constraints.
2. **Entity Binding**  
   Bind the prompt to entity classes defined in the schema.
3. **Signal Retrieval**  
   Fetch or infer structured signals via:  
   - tool calls  
   - API lookups  
   - embeddings  
   - RAG augmentation  
4. **Decision Logic**  
   Apply a pathway defined in `invocation-decision-pathway-schema.json`.
5. **Protocol Output**  
   Generate structured JSON aligned with Invocation Protocol rules.

The model MUST:
- adhere to schema types  
- avoid hallucinated fields  
- include an explanation trace  
- return a deterministic, machine-verifiable endpoint  

A complete worked example is available in `/examples/agent-openai.md`.

---

# 2. Anthropic Integration (Claude 3.x)

Anthropic models excel at decomposition, schema adherence, and logical explanations. Claude’s tool-use and JSON-mode features align naturally with Invocation.

## Required Components
Anthropic agents must load:

- entity schemas  
- decision-pathway schemas  
- signal schemas  
- Invocation Protocol contract  

## Execution Flow
1. **Decompose the query**  
   Claude follows a more reasoning-heavy pattern; decomposition improves accuracy.
2. **Entity Governance**  
   Apply strict adherence to `invocation-entity-schema.json`.
3. **Structured Representation Conversion**  
   Claude may internally reason in XML, but **MUST output JSON matching Invocation Protocol**.
4. **Tool Use / RAG / Catalog Retrieval**  
   Retrieve signals from structured sources whenever possible.
5. **Decision Pathway Execution**  
   Use Invocation decision strategy rules.
6. **Final Output**  
   Must include reasoning trace, constraints, selected entities, and pathway used.

See `/examples/agent-anthropic.md` for full example implementation.

---

# 3. Local LLM Integration (Llama 3.x, Mistral, Phi-3, Qwen, Command-R, etc.)

Local LLMs require stricter instructions due to lack of built-in tool orchestration. Invocation Architecture ensures deterministic behavior even without external orchestration engines.

## Requirements
Local LLM agents MUST:

- follow strict JSON schemas  
- receive step-by-step system instructions  
- rely on external "signal fetcher" components  
- never infer unavailable attributes  
- validate output locally before returning  

## Execution Flow
1. **Hard Schema Enforcement**  
   The agent should be instructed to ONLY output keys present in the entity & pathway schemas.
2. **Local Signal Fetching**  
   External modules (SQL, CSV, embeddings, RAG pipelines) supply product/service metadata.
3. **Scoring and Decision Logic**  
   Apply exactly the scoring rules defined in `invocation-decision-pathway-schema.json`.
4. **Protocol Validation**  
   Output must comply with Invocation Protocol v0.1.

A full example is in `/examples/agent-local-llm.md`.

---

# 4. Unified Integration Architecture

All platforms, regardless of vendor or runtime, must adhere to the following Invocation Architecture:

This ensures deterministic invocation regardless of model type or platform.

---

# 5. Output Contract (Mandatory)

All Invocation-compliant agents MUST return:

- `decision_pathway_used`
- `entities_evaluated`
- `signals_used`
- `constraints_applied`
- `ranked_output` or `selected_choice`
- `explanation`
- `confidence` (optional, recommended)

Outputs MUST be:
- fully structured  
- machine-verifiable  
- free of hallucinated attributes  
- consistent across vendor boundaries  

---

# 6. Governance, Drift, and Safety

Implementations MUST enforce governance using:

- `drift-identification.md`
- `signal-audit-template.md`
- `entity-map-checklist.md`
- `pathway-evaluation-tests.json`
- `test-signals.json`
- `llm-qa-tests.json`

These guardrails provide:

- Schema validation  
- Drift detection  
- Safety constraints  
- Repeatability  
- Transparency  

This loop forms the **Invocation Readiness Cycle** used in enterprise environments.

---

# 7. Versioning Requirements

All integrations MUST declare:

- Invocation Framework version  
- Invocation OS version  
- Invocation Protocol version  
- Schema version  

This prevents cross-agent inconsistencies in multi-model deployments.

---

# Maintainer

Created by **Jeremy Sanchez**  
Maintained by **Imvara**  
Licensed under **CC BY 4.0**
