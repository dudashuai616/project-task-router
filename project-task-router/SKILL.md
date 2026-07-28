---
name: project-task-router
description: Assess and route substantial tasks before execution by classifying complexity, clarifying boundaries, choosing direct work versus an in-thread plan versus separate conversations, defining dependencies and completion criteria, and creating compact handoffs. Use when a task is ambiguous, multi-step, likely to produce several deliverables, spans project stages or files, depends on upstream decisions, may create a long or noisy context, starts or resumes a long-running project, or needs continuity across conversations. Do not use for simple single-output tasks with clear scope.
---

# Project Task Router

Route work into the smallest reliable structure before producing large outputs. Preserve continuity through project files and compact handoffs rather than old chat transcripts.

## Run the complexity gate

Classify the task with the least ceremony needed:

- **Simple:** One clear outcome, little dependency risk, and no durable handoff need. Execute directly without showing a plan.
- **Focused multi-step:** One main deliverable with a few related steps. Give a short 2–5 step plan and continue in the same conversation.
- **Multi-stage:** Several distinct deliverables, different reference sets, or clear upstream/downstream dependencies. Propose phases and conversation boundaries before producing the full body of work.
- **Long-running:** Work is likely to span sessions, accumulate many decisions, or exceed reliable conversational context. Establish sources of truth, phase status, and a handoff method before execution.

Use observable evidence rather than pretending to know an exact remaining-context percentage. Warning signs include repeated revisions, many files or artifacts, difficulty checking early constraints, summarized earlier turns, and a phase transition that changes the required reference set.

## Decide conversation boundaries

Keep work in the same conversation when it is tightly coupled, iterates on the same artifact, or can finish reliably with the same small context set.

Recommend a new conversation when at least one of these is true:

- the current phase produces a stable artifact consumed by a different phase;
- the next phase needs substantially different files or expertise;
- independent review of one deliverable is valuable;
- continuing would carry large amounts of discarded exploration, logs, or rejected drafts;
- a compact file-based handoff can replace the transcript safely.

Do not split mechanically. A new conversation is justified only when it reduces context load, rework, or ambiguity. Recommend separate conversations and provide starter prompts, but do not create or fork user-owned tasks unless the user explicitly asks.

## Present the routing card

For multi-stage or long-running work, pause bulk execution and present a concise routing card containing:

1. **Overall goal** — one sentence.
2. **Recommended phases** — ordered by dependency.
3. **Conversation boundary** — same or new conversation for each phase, with one-line reasoning.
4. **Inputs** — exact upstream files or confirmed decisions to read; avoid broad project scans.
5. **Outputs** — named deliverables and their proper project location.
6. **Done when** — observable completion criteria.
7. **Handoff update** — which status, decision, or source-of-truth file must be updated.

If decomposition materially changes scope or sequencing, obtain the user's agreement before executing later phases. When the first phase is already clearly authorized, begin only that phase after presenting the structure.

## Preserve a source-of-truth chain

Treat chat as working space, not the authoritative archive.

- Follow applicable `AGENTS.md` and existing project organization.
- Read only the exact files needed for the current phase.
- Store accepted results in clearly named files inside the content's real project.
- Put each durable fact in one authoritative location; reference it elsewhere instead of duplicating it.
- Record only decisions that affect later work. Do not preserve hidden reasoning, discarded drafts, or verbose transcript summaries.
- When an upstream decision changes, identify downstream deliverables that require review and mark them clearly in project status.

Prefer an existing project status or decision file. If none exists and meaningful cross-session work requires one, propose the smallest useful file set rather than creating an index for every project.

## Create a compact handoff

Before changing conversations, pausing unfinished work, or continuing after context reliability declines, update formal artifacts first and then prepare a compact handoff with:

- task and current phase;
- completed and accepted work;
- locked decisions;
- authoritative file paths and versions;
- unfinished work and blockers;
- immediate next action;
- exact files the next conversation should read;
- a ready-to-use starter prompt for the next conversation.

Keep the handoff short enough to scan quickly. The next conversation should resume from formal files and the handoff, not reconstruct the old transcript.

## Starter-prompt pattern

Use this structure when recommending a new conversation:

```text
Continue [project], phase: [phase name].

Read and follow:
1. [applicable AGENTS.md]
2. [project source of truth]
3. [current status or handoff]
4. [exact upstream artifact or relevant section]

Do not read: [irrelevant chats, folders, or drafts].

Goal: [single phase goal].
Output: [named deliverable and location].
Done when: [observable criteria].
After completion: [status/decision/handoff updates].
```

## Keep overhead proportional

- Do not announce a complex workflow for a simple request.
- Do not create planning files that have no future consumer.
- Do not reread entire projects when exact sources are known.
- Do not continue producing later-stage assets before required upstream decisions are stable.
- Do not use subagents or parallel agents unless the user explicitly requests delegation or applicable instructions require it.

When this skill materially changes execution, tell the user briefly that the task is being split or handed off and why.
