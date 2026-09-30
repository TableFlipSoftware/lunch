# Landscape: what already exists

Researched 2026-09-30. Star counts are approximate. Items marked *unverified* came from search snippets or marketing copy.

**Bottom line:** no single tool does what Lunch aims to do, but most of the pieces already exist in separate, small projects.

## Tools that join Spec Kit (or OpenSpec) and Superpowers

None of these tries to make the documents shorter or less repetitive. They focus on handing work off between the two tools, or on resuming work later.

| Project | What it does | Maturity |
|---|---|---|
| [speckit-superpowers-bridge](https://github.com/lihan3238/speckit-superpowers-bridge) | A thin handoff: Spec Kit owns the design, Superpowers runs the implementation. Already used in Bellhop. | ~44★, v1.3.0, in the Spec Kit catalog |
| [SuperB](https://github.com/RbBtSn0w/spec-kit-extensions/tree/main/superpowers-bridge) | Runs Superpowers' brainstorming, implementation gate and critique at fixed points in the Spec Kit workflow | ~33★, v1.6.0 |
| [Superspec](https://github.com/WangX0111/superspec) | Six-phase Spec Kit + Superpowers flow that falls back to built-in behavior when Superpowers isn't installed | ~75★ |
| [cc-spex](https://github.com/rhuss/cc-spex) | Seven Spec Kit extensions: gates, deep review, collab, worktrees, teams, detach | ~120★, active |
| [Comet](https://github.com/rpamis/comet) | OpenSpec + Superpowers driven by a state machine; one `.comet.yaml` per change | ~3.1k★, v0.4.0 |

## Tools that make the documents easier to read or review

| Project | What it covers | Limit |
|---|---|---|
| [SpecKit Companion](https://speckit-companion.dev) ([post](https://www.alfredo-perez.dev/blog/2026-09-28-give-spec-kit-superpowers)) | One-page overview per spec, PR-style comments on spec lines, process sized to the change. The author writes: "you read all of them, and in practice nobody does." | Needs VS Code. The "60–68% leaner" claim is *unverified*. Announced 2026-09-28. **The closest overlap with Lunch.** |
| cc-spex `spex-collab` | Writes `REVIEWERS.md` (why / what / how), aiming for a PR you can review in about 30 minutes | Doesn't limit the spec, plan or tasks themselves |
| [speckit-tldr](https://github.com/qurore/speckit-tldr) | Turns spec + plan into a review-oriented TLDR: decisions, open questions, what changed in the PR | 3★, very early |
| [Token Budget](https://github.com/tinesoft/spec-kit-token-budget) | Squeezes artifacts after they're written, 40–50% smaller | Aimed at token cost, not human readers |
| [TinySpec](https://github.com/Quratulain-bilal/spec-kit-tinyspec) | One file of up to 80 lines replaces spec, plan and tasks | Small changes only |
| [PR Bridge](https://github.com/Quratulain-bilal/spec-kit-pr-bridge-) | Builds a PR description, a reviewer checklist and a map from requirements to code | 9★, a single commit |
| [Spec Kit lean preset](https://github.com/github/spec-kit/tree/main/presets/lean) | Official; shortens the process | Doesn't remove repetition between documents |
| [Superpowers PR #2333](https://github.com/obra/superpowers/pull/2333) | Merged 2026-09-25: "a plan is decisions, not a transcript". Plans come out about a third of their old size. | Plans only |
| [OpenSpec](https://github.com/Fission-AI/OpenSpec) delta specs | Each change records only what it adds, changes or removes, and is later merged into living specs | Still four files per change, and those files overlap each other |
| [explain-diff](https://github.com/studiokyoung/claude-skills) | One row per logical change, with evidence and a keep / cut / trim / ask verdict | 0★ |
| Kiro [bugfix spec](https://kiro.dev/docs/specs/) | A "what must remain unchanged" section | Kiro specs are otherwise verbose |

The [Spec Kit extension catalog](https://github.com/github/spec-kit/blob/main/docs/community/extensions.md) also lists changelog, ADR, archive, and reconcile/refine extensions. We saw only their one-line catalog descriptions.

## Criticism of the approach

- Böckeler, [martinfowler.com](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html): "I'd rather review code than all these markdown files." The process doesn't scale down to small problems.
- Marmelab, ["Waterfall Strikes Back"](https://marmelab.com/blog/2025/11/12/spec-driven-development-waterfall-strikes-back.html): reviewers hunt for mistakes hidden in verbose prose, and specs that contain code get reviewed twice.
- Spec Kit's own discussions say the same: [#1784](https://github.com/github/spec-kit/discussions/1784) ("the illusion of work") and [#411](https://github.com/github/spec-kit/discussions/411) (plan + tasks is "painfully redundant"). The only upstream fix so far is the lean preset.
- Superpowers issue [#2378](https://github.com/obra/superpowers/issues/2378): the brainstorming design doc has no template, so its layout varies from one feature to the next. The issue is still open.

## What's still missing

No tool does these, especially not together, and not in a way that works with any editor:

1. **Say each thing once.** Brainstorm doc, spec, plan, tasks and review notes each repeat the one before; nothing prevents that as they're written.
2. **Cap document length** so each one can be skimmed.
3. **One short summary per change for the reviewer**, linked to the decisions that drove it.
4. **Keep Superpowers' development habits**: test-first, subagents, code review.

"Shorter plans" alone is no longer a differentiator now that Superpowers PR #2333 has merged.

## Direction

- Build on the existing bridge setup, alongside the lean preset and PR #2333, instead of starting from scratch.
- Make gaps 1–3 Lunch's own contribution.
- Reuse or credit:
  - OpenSpec's added / modified / removed delta format;
  - cc-spex's `REVIEWERS.md` layout;
  - Kiro's "what must not change" section;
  - Marmelab's rule: no code in specs.
- Before building, try SpecKit Companion hands-on. If it holds up outside VS Code, Lunch could be a Spec Kit extension rather than a separate product.
