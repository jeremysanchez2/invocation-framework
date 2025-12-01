# Invocation Framework — Integration Specification

This document explains how the Invocation Framework integrates with:

- **OpenAI models**  
- **Anthropic Claude models**  
- **Local LLM / RAG-based agents**

---

# 1. OpenAI Integration (GPT-4.1, GPT-5, o-series)

OpenAI models follow a **function-first**, **schema-guided**, **tool-enabled** workflow.

## OpenAI Integration Components
- `invocation-entity-schema.json`
- `invocation-decision-pathway-schema.json`
- `invocation-signal-schema.json`
- Product/Service schemas
- Invocation Protocol v0.1

## Execution Flow
1. Parse domain + intent  
2. Bind entities using schemas  
3. Fetch structured signals  
4. Apply decision pathway  
5. Produce deterministic output  

See `/examples/agent-openai.md` for a full reference flow.

---

# 2. Anthropic Integration (Claude 3.x)

Claude models excel at:

- schema enforcement  
- logical decomposition  
- safety alignment  

Anthropic uses *XML mode*, *JSON mode*, and *Tool Use* for Invocation.

## Claude Integration Flow
1. Detect domain + constraints  
2. Apply Entity Governance  
3. Use XML → JSON schema conversion  
4. Execute reasoning + tool calls  
5. Return structured Invocation result  

See `/examples/agent-anthropic.md`.

---

# 3. Local LLM Integration

Local LLMs (Llama 3.x, Mistral, Phi-3) typically require:

- explicit system prompts  
- tight JSON schemas  
- minimal multi-step reasoning  

## Integration Flow
1. Hard-enforced schema bindings  
2. Local embeddings-based “signal fetcher”  
3. Deterministic scoring using decision-pathway-schema.json  
4. Output validation using Invocation Protocol  

See `/examples/agent-local-llm.md`.

---

# 4. Recommended Architecture Diagram
