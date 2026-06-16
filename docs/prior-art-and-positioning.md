# Prior Art And Positioning

## 1. Purpose

This document positions Brownyx CEL relative to existing ideas without claiming that every underlying concept is new.

CEL is a project-specific architecture pattern assembled for Brownyx.

## 2. What Is Not New

CEL is inspired by several existing families of ideas:

- cognitive architectures;
- metacognition;
- reflective agents;
- self-monitoring systems;
- hypothesis generation;
- frame switching;
- contradiction detection;
- question generation;
- analogical reasoning;
- bisociative creativity.

These ideas exist in cognitive science, AI research, philosophy of mind, creativity theory, and agent architecture.

## 3. What Is Project-Specific

The project-specific contribution is the Brownyx ordering and boundary discipline:

```text
direct reasoning
-> context sufficiency
-> intent clarification
-> frame switching
-> contradiction detection
-> hypothesis generation
-> self-model tension detection
-> question generation
-> analogy
-> bisociation
-> synthesis
```

This sequence is combined with explicit persistence boundaries:

- ordinary memory is not polluted by expansion candidates;
- self-model cannot be rewritten directly;
- bisociation is internal-only by default;
- hypotheses and contradictions become agenda work;
- durable questions are stored as questions;
- useful cognitive patterns may become MindCells;
- all expansions must return to clear synthesis.

## 4. Why This Matters

Many agent systems collapse too many internal phenomena into one prompt or one answer-generation step.

Brownyx CEL separates:

- direct answer generation;
- cognitive expansion;
- persistence;
- agenda work;
- self-model gates;
- user-facing synthesis.

This separation makes the system more inspectable and safer.

## 5. Suggested Public Positioning

Use this phrasing:

> Brownyx CEL is a project-specific cognitive expansion architecture for persistent synthetic mind runtimes. It combines frame switching, contradiction detection, hypothesis generation, self-model tension detection, question generation, analogy, and late-stage bisociation under strict trace, persistence, and clarity boundaries.

Avoid saying:

> We invented cognitive expansion.

Better:

> We define Brownyx CEL as a specific bounded architecture pattern for cognitive expansion in Brownyx-style synthetic mind runtimes.

## 6. Prior Art Statement

The public publication of this repository is intended to establish a clear timestamp for the specific Brownyx CEL architecture, terminology, sequencing, and persistence-boundary design.

It does not claim exclusive ownership of all underlying concepts.
