# Brownyx CEL Architecture

## 1. Position In The Runtime

CEL is designed as an optional bounded stage within the cognitive cycle.

Recommended position:

```text
event
  -> event intake
  -> salience and focus formation
  -> memory recall
  -> local/external knowledge context
  -> Cognitive Expansion Layer
  -> candidate action / response / reflection generation
  -> inhibition and policy checks
  -> self-model gate
  -> question synchronization
  -> viability update
  -> trace + artifact finalization
```

## 2. Main Components

### 2.1. Trigger Evaluator

Decides whether CEL should run.

Inputs:

- event type;
- salience;
- workspace focus;
- retrieved memory summaries;
- active questions;
- active agenda items;
- latest viability state;
- recent CEL history.

Output:

```text
CognitiveExpansionTrigger
```

### 2.2. Input Builder

Creates a compact bounded input for the structured CEL call.

Input should include:

- current event summary;
- recalled memory summaries;
- self-model summary;
- active questions;
- active agenda items;
- latest viability summary;
- workspace focus;
- inner-world summary if already available.

Do not include raw private trace internals unless needed for an operator-only diagnostic run.

### 2.3. Structured Expansion Runner

Runs one structured model call.

Output must be JSON.

The model is not the final voice of the Mind.

### 2.4. Validator

Rejects or clamps:

- invalid JSON;
- forbidden consciousness claims;
- direct self-model patches;
- new memory type requests;
- decorative metaphors with low usefulness;
- too many questions;
- high-risk bisociations;
- output that tries to bypass safety or policy.

### 2.5. Persistence Mapper

Maps strong candidates into existing Brownyx structures:

- Contradiction;
- Hypothesis;
- CognitiveAgendaItem;
- MindQuestion;
- MindCell;
- CycleTrace.

### 2.6. Synthesis Handler

Converts expansion into a plain internal or user-facing conclusion.

It must answer:

- what was detected;
- what was persisted;
- what was rejected;
- what should be reviewed;
- what should be shown to the user, if anything.

## 3. Persistence Philosophy

CEL is trace-first.

Most expansion candidates should remain in CycleTrace only.

Only durable and useful outputs should become agenda, hypotheses, contradictions, questions, MindCells, or artifacts.

## 4. Safety Philosophy

CEL expands cognition but does not override safety.

CEL must not bypass:

- inhibition;
- action policy;
- contact regulation;
- external executor permissions;
- self-model gates;
- lifecycle controls;
- operator stop/delete authority;
- cycle budgets.

## 5. Why No New Table In MVP

A new table such as `cognitive_expansion_runs` may be useful later, but the MVP should use CycleTrace and runtime_state summaries first.

Reason:

- fewer migrations;
- fewer state boundaries;
- less dashboard complexity;
- easier rollback;
- less risk of treating expansion as durable memory too early.

## 6. Future Optional Table

If trace-only storage becomes insufficient, add:

```text
cognitive_expansion_runs
```

Fields:

```text
id
mind_id
cycle_id
trace_id
event_id
trigger_reasons
strategies_used
summary
persisted_counts
risk_flags
created_at
```

Do not store raw prompts or private memory content in this table.
