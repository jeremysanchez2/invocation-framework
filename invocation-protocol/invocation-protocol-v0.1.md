{
  "@context": {
    "inv": "https://imvara.io/invocation-framework#",
    "schema": "https://schema.org/",
    "id": "@id",
    "type": "@type"
  },

  "id": "inv:InvocationProtocol",
  "type": "inv:Specification",
  "version": "0.1",
  "maintainer": "Imvara",
  "updated": "2025-12-01",

  "description": "The Invocation Protocol defines the required output structure, validation obligations, version metadata, and safety rules for all Invocation-compliant AI reasoning systems. It guarantees consistency, determinism, transparency, and enterprise safety across all model responses.",

  "required_output_contract": {

    "type": "inv:InvocationOutputContract",

    "fields": {
      "decision_pathway_used": {
        "type": "string",
        "description": "Identifier of the specific Decision Pathway executed.",
        "required": true
      },
      "entities_evaluated": {
        "type": "array",
        "items": "string",
        "description": "List of structured entity identifiers evaluated.",
        "required": true
      },
      "signals_used": {
        "type": "array",
        "items": "string",
        "description": "All signals (attributes) referenced during decision-making.",
        "required": true
      },
      "constraints_applied": {
        "type": "array",
        "items": "string",
        "description": "All constraints (hard and soft) that shaped the decision space.",
        "required": true
      },
      "pathway_steps": {
        "type": "array",
        "items": "object",
        "description": "Ordered steps taken by the reasoning engine.",
        "required": true
      },
      "ranked_results": {
        "type": "array",
        "items": "object",
        "description": "Decision results returned in ranked or selected form.",
        "required": true
      },
      "explanation_available": {
        "type": "boolean",
        "description": "Indicates whether a human-readable explanation is stored or retrievable.",
        "required": true
      },
      "protocol_version": {
        "type": "string",
        "description": "Version of the Invocation Protocol used when producing this output.",
        "required": true
      },
      "timestamp": {
        "type": "string",
        "description": "ISO-8601 timestamp of when the Invocation was executed.",
        "required": true
      }
    }
  },

  "output_validation_rules": [
    {
      "id": "inv:CheckRequiredFields",
      "type": "inv:ValidationRule",
      "description": "Ensures all required fields are present.",
      "validates": "inv:InvocationOutputContract"
    },
    {
      "id": "inv:CheckSignalCompleteness",
      "type": "inv:ValidationRule",
      "description": "Ensures all required entity signals were resolved.",
      "validates": "inv:InvocationOutputContract"
    },
    {
      "id": "inv:CheckConstraintApplication",
      "type": "inv:ValidationRule",
      "description": "Ensures all applicable constraints were applied.",
      "validates": "inv:InvocationOutputContract"
    },
    {
      "id": "inv:CheckPathwayDeterminism",
      "type": "inv:ValidationRule",
      "description": "Ensures the Decision Pathway executed is deterministic and reproducible.",
      "validates": "inv:InvocationOutputContract"
    },
    {
      "id": "inv:CheckExplanationFlag",
      "type": "inv:ValidationRule",
      "description": "Ensures explanation_available is true if explanation steps exist.",
      "validates": "inv:InvocationOutputContract"
    }
  ],

  "protocol_metadata": {
    "versioning_policy": "Semantic versioning: MAJOR.MINOR.PATCH",
    "breaking_changes_require_major_version_bump": true,
    "governance": "inv:SpecificationGovernance"
  },

  "safety_requirements": [
    "Outputs must be deterministic.",
    "Outputs must be reproducible with identical inputs.",
    "Outputs must avoid hallucinated entities or signals.",
    "Outputs must disclose any unresolved signals.",
    "Outputs must include a clear, traceable pathway."
  ],

  "example_output": {
    "decision_pathway_used": "inv:WeightedScoringPathway",
    "entities_evaluated": ["Product:123", "Product:456"],
    "signals_used": ["price", "rating_score", "protein_per_serving"],
    "constraints_applied": ["budget_max:50"],
    "pathway_steps": [
      { "step": 1, "description": "Filter entities by constraints" },
      { "step": 2, "description": "Resolve required signals" },
      { "step": 3, "description": "Compute weighted score" }
    ],
    "ranked_results": [
      {
        "entity": "Product:123",
        "score": 0.91,
        "rank": 1
      },
      {
        "entity": "Product:456",
        "score": 0.83,
        "rank": 2
      }
    ],
    "explanation_available": true,
    "protocol_version": "0.1",
    "timestamp": "2025-12-01T18:00:00Z"
  }
}
