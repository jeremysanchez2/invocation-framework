# Imvara Invocation Framework — Developer Documentation  
Welcome to the official documentation for the **Invocation Framework**, an open standard for deterministic, explainable AI reasoning created and maintained by **Imvara**.

Invocation transforms natural-language intent into **validated, governed machine decisions**, using structured schemas, deterministic pathways, and strict validation rules.

This documentation includes:

- Conceptual overviews  
- Implementation guides  
- Canonical references  
- Specifications  
- Examples and patterns  
- Testing and compliance resources  

Whether you're building LLM agents, enterprise AI systems, or reasoning engines, this framework gives you a reliable, governed foundation.

---

# 1. What Is Invocation?

Invocation is the structured process of transforming:

```text
Intent → Entities → Signals → Decision → Validated Output
```

Unlike typical LLM reasoning, Invocation is:

- **Deterministic**  
- **Schema-bound**  
- **Explainable**  
- **Governed**  
- **Reproducible**  

Invocation ensures AI systems behave the same way, every time, for the same inputs.

---

# 2. Quick Start

To understand Invocation quickly, begin here:

- [`quickstart.md`](quickstart.md) — The fastest way to understand Invocation  
- [`spec-index.md`](spec-index.md) — The specification entrypoint  
- [`../specs/examples/`](../specs/examples/) — Real Invocation patterns  

---

# 3. Core Specifications

The Invocation Framework is defined by five canonical specifications:

- [`spec-architecture.md`](spec-architecture.md)  
- [`spec-governance.md`](spec-governance.md)  
- [`spec-pathways.md`](spec-pathways.md)  
- [`spec-validation.md`](spec-validation.md)  
- [`spec-index.md`](spec-index.md) *(overview document)*  

These documents define the formal rules for Invocation-compliant systems.

---

# 4. Canonical Schema Registry

Schemas define the structure of entities, signals, products, services, decisions, constraints, and pathways.

The schema registry lives under:

```
/specs/schemas/
```

Start with:

- `invocation-entity-schema.json`  
- `invocation-signal-schema.json`  
- `invocation-decision-pathway-schema.json`  

---

# 5. Examples & Patterns

Real-world Invocation examples are located at:

```
/specs/examples/
```

These show how Invocation works for:

- Retail product comparison  
- Automotive selection  
- Insurance plan recommendation  
- Hospitality selection  
- Agent implementations (OpenAI, Anthropic, Local LLM)

---

# 6. Compliance & Testing

Compliance resources live under:

```
/tests/
```

This includes:

- Schema validation tests  
- Pathway determinism tests  
- Output protocol tests  

Systems MUST pass all tests to claim Invocation compliance.

---

# 7. License

Documentation and specifications are licensed under:

**Creative Commons Attribution 4.0 (CC BY 4.0)**

---

## About Imvara

Imvara is the creator and maintainer of the Invocation Framework — an open standard for AI reasoning and decision architecture.

Learn more at **https://imvara.io**
