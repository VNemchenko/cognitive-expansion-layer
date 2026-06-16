# Brownyx CEL Technical Specification

## 1. Name

**Brownyx Cognitive Expansion Layer**  
Short name: **Brownyx CEL**

## 2. Scope

CEL is a bounded optional internal stage in the Brownyx cognitive cycle.

It should run after recall/context assembly and before final response/action selection.

## 3. Core Rule

```text
Direct reasoning first.
Expansion only when justified.
Bisociation only as a late-stage strategy.
Synthesis always last.
```

## 4. Trigger Rules

CEL may run when at least one condition is true:

- event salience is high;
- the input asks for diagnosis, design, architecture, strategy, meaning, or project direction;
- the cycle detects ambiguity;
- retrieved contexts conflict;
- there are active unresolved questions;
- there is possible self-model relevance;
- Agenda v2 selected a hypothesis, contradiction, research request, or self-model tension;
- latest viability state indicates stagnation risk or unresolved tension pressure.

CEL should be skipped when:

- the event is a low-signal internal tick;
- the task is a simple factual or operational answer;
- there is already a sufficient direct answer;
- cycle budget is exhausted;
- LLM route is unavailable;
- recent CEL runs produced no material result;
- rumination risk is high.

## 5. Strategy Ladder

| Order | Strategy | Output |
|---:|---|---|
| 1 | Context Sufficiency Check | context gaps |
| 2 | Intent Clarification | intent summary |
| 3 | Frame Switching | frame candidates |
| 4 | Contradiction Detection | contradiction candidates |
| 5 | Hypothesis Generation | hypothesis candidates |
| 6 | Self-Model Tension Detection | tension candidates |
| 7 | Question Generation | question candidates |
| 8 | Analogy | analogy candidates |
| 9 | Bisociation | bisociation candidates |
| 10 | Synthesis | plain conclusion |

## 6. Suggested Service

```text
backend/app/services/cognitive_expansion.py
```

Suggested interface:

```python
class CognitiveExpansionService:
    def should_run(self, context) -> CognitiveExpansionTrigger:
        ...

    def build_input(self, context) -> CognitiveExpansionInput:
        ...

    def run(self, context) -> CognitiveExpansionResult:
        ...

    def validate_result(self, result) -> CognitiveExpansionResult:
        ...

    def apply_persistence(self, result) -> CognitiveExpansionPersistenceReport:
        ...

    def append_trace_step(self, result, report) -> None:
        ...
```

## 7. Suggested Schemas

```python
class CognitiveExpansionTrigger(BaseModel):
    should_run: bool
    reasons: list[str]
    skipped_reason: str | None = None
    max_strategy_level: str | None = None

class CognitiveExpansionResult(BaseModel):
    should_run: bool
    trigger_reasons: list[str] = []
    strategies_used: list[str] = []
    context_gaps: list[str] = []
    intent_summary: str | None = None
    frames: list[FrameCandidate] = []
    contradictions: list[ContradictionCandidate] = []
    hypotheses: list[HypothesisCandidate] = []
    self_model_tensions: list[SelfModelTensionCandidate] = []
    questions: list[QuestionCandidate] = []
    analogies: list[AnalogyCandidate] = []
    bisociations: list[BisociationCandidate] = []
    synthesis: str
    recommended_output_mode: str
    confidence: float
```

## 8. Persistence Mapping

### Contradictions

Persist only if:

```text
severity >= 0.55
confidence >= 0.55
```

Target:

```text
Contradiction
CognitiveAgendaItem(type="contradiction")
```

### Hypotheses

Persist only if:

```text
confidence >= 0.35
novelty >= 0.35
```

Target:

```text
Hypothesis
CognitiveAgendaItem(type="hypothesis_seed")
```

### Self-Model Tensions

Persist as agenda only:

```text
CognitiveAgendaItem(type="self_model_tension")
```

Do not directly write SelfModelVersion.

### Questions

Persist only if durable and non-duplicative:

```text
MindQuestion
CognitiveAgendaItem(type="open_question")
```

### Analogies

Persist only if clear and useful:

```text
clarity_score >= 0.70
usefulness_score >= 0.60
risk_score <= 0.50
```

Target:

```text
CycleTrace
MindCell if durable
Artifact candidate if appropriate
```

### Bisociations

Persist only if strict quality thresholds pass:

```text
clarity_score >= 0.75
usefulness_score >= 0.70
risk_score <= 0.45
```

Default:

```text
internal only
```

## 9. Trace Step

CEL should append a trace step named:

```text
cognitive_expansion
```

Example:

```json
{
  "step": "cognitive_expansion",
  "enabled": true,
  "should_run": true,
  "trigger_reasons": [],
  "strategies_used": [],
  "result_summary": "",
  "persisted": {
    "contradictions": [],
    "hypotheses": [],
    "agenda_items": [],
    "questions": [],
    "mind_cells": []
  },
  "skipped_reason": null,
  "llm_used": true,
  "model": "...",
  "validation_errors": []
}
```

## 10. Acceptance Criteria

CEL is accepted when:

1. It does not run on every simple cycle.
2. It runs on high-signal ambiguous, diagnostic, self-model, contradiction, research, or creative cycles.
3. It produces structured validated JSON.
4. Results are stored in CycleTrace.
5. Strong contradictions create existing Contradiction records.
6. Strong hypotheses create or update existing Hypothesis records.
7. Self-model tensions create agenda items, not direct self-model versions.
8. Durable questions are synchronized into MindQuestion.
9. Analogies and bisociations are internal-only by default.
10. User-facing output remains clear.
11. The system does not claim consciousness.
12. No new memory types are introduced.
