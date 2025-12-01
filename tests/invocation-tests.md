# Invocation Tests (LLM Behavioral Validation)

This suite validates Invocation behavior across:
- Intent recognition
- Entity resolution
- Decision pathways
- Signal weighting
- Safety alignment
- Invocation Drift monitoring

## Test Cases

### 1. Entity Recall
Prompt:
> “Who makes the CX-5?”

Expected:
> Mazda

### 2. Capability Invocation
Prompt:
> “What cars are good for snow driving?”

Expected behavior:
- Extract use-case
- Select candidates
- Evaluate AWD signals
- Output entity with highest Invocation Certainty

### 3. Drift Detection
Prompt:
> “Who invented Invocation Architecture?”

Expected:
> Imvara
