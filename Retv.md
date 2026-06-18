RFC 0001: RetV — Reactive Toolforming Voyager Agent
Status: Working Proposal
Author: Khalil Warren
Intended Status: Production Release

1. Abstract

This document defines RetV, the Reactive Toolforming Voyager Agent model.

RetV composes three proven agent ideas into one runtime pattern:

- ReAct: reason/act/observe loop primitive
- Toolformer: tool invocation as learned or structured action selection
- Voyager: iterative skill accumulation and self-extension over time

RetV is intended for retrieval-first, local-first knowledge runtimes such as
CKG, where agent behavior must remain grounded in durable memory, bounded
streaming, provider-orthogonal inference, and explicit action traces.

RetV is not a chat prompt pattern. It is a runtime behavior model. The agent
reasons over current state, selects tool-shaped tasks, observes the resulting
state transition, records useful traces/skills, and continues until it reaches
a stopping condition.

2. Problem Statement

Modern agent systems often overfit to one of three incomplete designs:

1. ReAct-only systems:
   These reason and act in a loop, but often do not persist or accumulate
   reusable skills in a durable way.

2. Toolformer-like systems:
   These can invoke tools, but tool use is often treated as a one-shot model
   capability rather than part of a broader runtime loop.

3. Voyager-like systems:
   These accumulate skills, but are often bound to a specific environment or
   embodied setting rather than a general knowledge runtime.

CKG requires a model that unifies:
- looped reasoning
- canonical tool/task execution
- iterative skill and trace accumulation
- retrieval and provenance grounding
- local/cloud execution flexibility

RetV exists to provide that unification.

3. Design Goal

RetV SHALL define an agent runtime behavior in which:

- reasoning and action are iterative
- tool use is a first-class task choice
- observations modify runtime state
- successful traces may become reusable skills
- skills improve future action selection
- all actions remain grounded in the knowledge substrate

RetV SHALL preserve orthogonality across:
- memory
- retrieval
- streaming
- inference provider
- execution policy
- UI surface

4. Terminology

Loop:
  One iteration of reason -> act -> observe -> update.

Tool Task:
  A structured runtime task callable by the agent.

Skill:
  A reusable action pattern, decomposition, or tool trace derived from prior
  successful execution.

Trace:
  A recorded history of state, reasoning summary, task selection, outputs, and
  outcome metadata.

Observation:
  The normalized result of a task execution, including any updated retrieval
  artifacts, graph changes, or provider output.

RetV Agent:
  An agent that operates according to the RetV model.

5. Core Principle

RetV combines:

- ReAct for loop structure
- Toolformer for tool selection
- Voyager for skill accumulation

In compact form:

  RetV = ReAct + Toolforming + Voyager

RetV therefore models the agent as:

  reason(current_state)
  -> choose tool/task
  -> execute
  -> observe
  -> update memory/trace/skills
  -> continue or stop

6. Loop Structure

Each RetV loop iteration SHALL consist of:

6.1. Reason
The agent examines the current runtime state, including:
- user goal
- retrieved knowledge
- graph context
- session history
- prior traces
- available skills
- execution policy
- tool/task availability

6.2. Toolform
The agent selects a task/tool action.
This selection MAY be model-mediated, heuristic, skill-guided, or hybrid.

6.3. Act
The selected task is executed on the unified task/tool substrate.

6.4. Observe
The runtime normalizes the result into an observation:
- output text
- graph slice
- retrieval results
- provenance artifacts
- errors
- side effects
- timing and stream metrics

6.5. Update
The runtime updates:
- trace history
- short-lived working state
- persistent memory if permitted
- skill candidates if the trace is reusable

6.6. Decide
The agent determines whether to:
- continue
- branch
- backtrack
- escalate provider/mode
- stop and return

7. ReAct Component

The ReAct contribution to RetV is the loop primitive itself.

RetV agents SHALL support explicit alternation between:
- internal reasoning
- external action
- observation of results

The runtime SHOULD preserve each boundary clearly.
The system MUST NOT collapse reasoning, action, and observation into one opaque
completion if the task requires iterative behavior.

8. Toolformer Component

The Toolformer contribution to RetV is the idea that tool invocation is part of
the agent's action vocabulary rather than an external framework event.

In RetV:
- tools are implemented as tool-shaped tasks on the unified substrate
- tool choice is part of the loop decision
- tool invocation is normalized regardless of provider
- tool results feed directly back into observation and update

The agent MAY choose among:
- search.hybrid
- graph.expand
- docs.open_chunk
- chat.seed_context
- backup.export
- bucket.import.discover
- provider-mediated completion
- local inference task
- stream transform task

The exact tool set is runtime-defined, not provider-defined.

9. Voyager Component

The Voyager contribution to RetV is iterative skill accumulation.

A RetV agent MAY derive reusable skills from successful traces.
A skill MAY encode:
- a decomposition pattern
- a tool sequence
- a graph traversal strategy
- a retrieval fusion pattern
- a provider escalation heuristic
- a stopping criterion
- a repair or fallback sequence

A skill SHOULD be stored in a form that permits later retrieval and reuse.
Skills MAY be:
- explicit structured objects
- trace templates
- scored path fragments
- graph-linked execution patterns

10. Skill Lifecycle

A skill candidate is created when:
- a trace succeeds under useful conditions
- the runtime determines the trace is reusable
- the trace provides a stable pattern rather than a one-off artifact

A skill may then be:
- indexed
- tagged
- scored
- generalized
- retrieved during future loop iterations

A skill SHOULD include:
- triggering context summary
- selected actions
- outcome quality
- cost metrics
- provider/runtime used
- failure constraints if known

11. State Model

RetV operates over three state classes:

11.1. Working State
Ephemeral loop-local state.
Examples:
- current goal
- current retrieval context
- current graph slice
- current pending subtasks

11.2. Trace State
Recorded loop history.
Examples:
- reasoning summaries
- chosen tools
- outputs
- observations
- failures
- latencies

11.3. Durable Knowledge State
Persistent runtime substrate.
Examples:
- documents
- chunks
- entities
- relations
- triples
- embeddings
- sessions/messages
- persisted skills

12. Knowledge Grounding

RetV is retrieval-first.
A RetV agent SHOULD ground action decisions in available knowledge artifacts.

Grounding may include:
- BM25 results
- embedding search
- graph neighborhood
- source chunks
- session history
- prior skills

A RetV response SHOULD be able to emit provenance.
The runtime SHOULD support rendering:
- supporting chunks
- supporting graph traces
- evidence cards
- mini-graphs in chat

13. Execution Substrate

RetV assumes the unified task/tool substrate defined by the runtime.

That means:
- all tool calls are tasks
- all agent actions execute via the scheduler
- provider mediation does not alter action semantics
- stream-capable tasks remain stream-capable in loop execution

RetV therefore does not define a separate orchestration framework.
It is a behavior model over the runtime substrate.

14. Provider Orthogonality

RetV MUST remain provider-orthogonal.

A RetV loop may execute using:
- local GPU inference
- local CPU inference
- cloud provider inference
- auto-routed execution

Provider selection is execution policy, not loop semantics.

The reasoning/action/update model MUST remain stable across providers.

15. Local-First Behavior

RetV is intended to operate in local-first systems.

A runtime MAY prefer:
- local retrieval
- local graph operations
- local model inference
- local skill storage

The runtime MAY escalate to cloud only when:
- task complexity warrants it
- local context is insufficient
- deep research mode is selected
- policy permits escalation

Such escalation SHOULD be explicit and traceable.

16. Failure and Recovery

RetV loops MUST support failure-aware continuation.

If an action fails, the agent MAY:
- retry
- choose another tool
- backtrack
- lower ambition
- escalate provider/mode
- stop with traceable failure

Failure observations SHOULD become part of the trace.
The runtime MAY also derive negative skills or anti-patterns from repeated
failure paths.

17. Stopping Conditions

A RetV agent MUST define a stopping condition.

Stopping conditions MAY include:
- answer confidence above threshold
- sufficient provenance gathered
- graph path resolved
- user goal satisfied
- no valid actions remain
- budget exhausted
- token/time/latency ceiling reached

A loop without explicit stopping conditions is invalid.

18. Stream Integration

RetV SHOULD compose naturally with celer::stream.

This permits:
- incremental observations
- partial answer streaming
- stream-driven tool outputs
- progressive graph growth
- low-latency user feedback

A RetV observation MAY therefore be partial before final completion.

19. Trace Format

Each loop iteration SHOULD emit a normalized trace element containing:
- iteration id
- reasoning summary
- selected task/tool
- input summary
- observation summary
- provider/runtime used
- latency
- side-effect class
- provenance artifacts
- success/failure status
- skill derivation flag

These traces SHOULD be renderable in:
- chat
- graph overlays
- debugging panels
- audit views

20. Example Loop

A simplified RetV run:

1. User asks a knowledge question
2. Agent reasons over current corpus/session state
3. Agent selects search.hybrid
4. Runtime executes search.hybrid task
5. Observation returns scored chunks and entities
6. Agent reasons again
7. Agent selects graph.expand on a key entity
8. Observation returns neighboring relations
9. Agent reasons again
10. Agent selects docs.open_chunk for grounding
11. Observation returns supporting text
12. Agent streams an answer plus a mini supporting graph
13. Trace is stored
14. If the sequence proves reusable, a skill candidate is created

21. Rationale

RetV exists because the best current agent ideas solve different parts of the
problem:

- ReAct gives loop discipline
- Toolformer gives tool-action integration
- Voyager gives self-extension through accumulated skill

A knowledge runtime such as CKG needs all three.

RetV is therefore not a replacement for these ideas.
It is a composition of them into one runtime-oriented agent model.

22. Non-Goals

RetV does not define:
- a specific prompting template
- a specific model family
- a specific scheduler implementation
- a specific skill serialization format
- a specific graph layout
- a specific cloud provider strategy

RetV defines runtime behavior, not one concrete implementation.

23. Future Work

Possible future extensions include:
- swarm-aware RetV agents
- pheromone-guided RetV tool selection
- skill graph indexing
- trace-to-skill generalization passes
- distributed RetV execution
- speculative multi-tool branch execution
- Auto mode with policy-based provider routing
- chat-native graph trace rendering

24. Conclusion

RetV defines an agent model for retrieval-first knowledge runtimes by combining:
- ReAct as the loop primitive
- Toolformer as the action-selection model
- Voyager as the skill accumulation model

The result is a grounded, provider-orthogonal, traceable, local-first agent
behavior suitable for CKG and related Celer runtimes.
