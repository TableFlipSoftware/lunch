# Flow: the human layer

Agreed 2026-09-30. This supersedes the "Direction" section of [landscape.md](landscape.md), which assumed Lunch would constrain the upstream documents.

## Principle

Working documents (brainstorm, spec, plan, tasks) may be as long and repetitive as the LLM needs. Lunch adds a **human layer**: at every point where a person has to read, decide or approve, they get a short digest in the conversation, with a diagram where structure matters. The person should never have to open the spec folders to follow along.

## Flow

```
 HUMAN                     LUNCH (human layer)                 UPSTREAM (working layer)
 ─────                     ───────────────────                 ────────────────────────

 "add feature X"  ──▶ GATE 0: is the prompt ready?
                       who is it for / what problem /
                       what does done look like
                              │
                ┌─────────────┴──────────────┐
                │ ready                       │ thin
                │                             ▼
                │                   BRAINSTORM (Superpowers)
                │                   explore intent + design
                │                   with the human, in chat
                │                             │
                │  human  ◀──── DIGEST 0 ─────┤
                │  confirms     (what we'll   │
                │               build, why)   │
                └─────────────┬───────────────┘
                              ▼
                     refined feature description
                              │
                              └───────────────────────────▶ specify / clarify
                                                            writes spec folder
                                                            (long, repetitive, fine)
                                      ┌─────────────────────────────┘
                                      ▼
                           DIGEST 1: what we're building,
                           open questions (self-contained),
                           diagram: where X fits in system
                                      │
 answers in chat  ◀───────────────────┘
        │  ─ ─ ─ expand? ─ ─ ─▶ show one section verbatim from file
        ▼
 answers ─────────────────────────────────────────────────────▶ plan / tasks
                                                               writes plan + task files
                                      ┌─────────────────────────────┘
                                      ▼
                           DIGEST 2: approach, order of work
                           (small diagram, no task list)
                                      │
 approves  ◀──────────────────────────┘
        │
        ▼
 approves ────────────────────────────────────────────────────▶ implement
                                                               (Superpowers: TDD, subagents,
                                                                code review)
                                      ┌─────────────────────────────┘
                                      │  only decisions and surprises
                                      ▼  that need the human
                           DIGEST 3 (as needed)
                                      │
 decides  ◀───────────────────────────┘
                                                               done
                                      ┌─────────────────────────────┘
                                      ▼
                           PR PACKET (committed, Mermaid)
                            1. concise design + change summary
                            2. before/after diagrams
                            3. updated product-level spec
                                      │
                                      ▼
 code reviewer  ◀──────── PR ─────────┘
```

## Decisions

- **Digests are built from the files, not from memory.** They can't contradict the working documents.
- **Expand shows one section verbatim.** It never regenerates a longer version. Cost is a few hundred extra output tokens per digest, offset by suppressing upstream's own verbose chat summary.
- **Stay in the console.** Leave it (Artifact or a file) only when a rendered page is clearly easier to understand, and say why.
- **Diagram format:** text diagrams in the console, Mermaid in committed files and the PR.
- **Each clarify question stands alone,** with options and a recommendation, so it can be answered without opening `spec.md`.
- **Wrap, don't fork.** Each upstream step runs as normal, then Lunch digests its result (per [CLAUDE.md](../CLAUDE.md)). Works on top of Spec Kit or OpenSpec.
- **Gate 0 is a short checklist, not a trained classifier.**

## Why Gate 0

Checked against Spec Kit `main` on 2026-09-30: nothing in it judges whether a prompt is too thin.
- `specify` guesses from context, allows at most 3 `[NEEDS CLARIFICATION]` markers, and errors only when it finds no user flow.
- `clarify` asks at most 5 short questions about gaps in an existing spec. It doesn't explore alternatives or challenge the idea.

A thin prompt therefore becomes a spec built on assumptions. Brainstorming first gives `specify` a description the human has already agreed to. Spec Kit's `before_specify` hook is one place to attach the gate.

## Open questions

- Is the PR packet a committed file, or only the PR description?
- Does the product-level spec describe behavior, structure, or both? Spec Kit has no product-level spec. OpenSpec's living specs record behavior only.
- Stay tool-agnostic (Spec Kit or OpenSpec), or pick one and go deeper?
