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

## Architecture diagrams

Checked against both repos' `main` on 2026-09-30.

Neither tool draws an architecture diagram by default. Spec Kit's `plan-template.md` shows structure only as a directory tree ("Project Structure"). OpenSpec's `design.md` template has four sections (Context, Goals/Non-Goals, Decisions, Risks/Trade-offs) and no diagram section.

| Source | What it draws | Limit |
|---|---|---|
| [Data Model Diagram](https://github.com/benizzio/spec-kit-data-model-diagram) (Spec Kit extension) | Mermaid ER diagram made from `data-model.md` | Data model only |
| [ASCII Diagram Renderer](https://github.com/MRZHUH/spec-kit-ascii-diagram) (Spec Kit extension) | Text diagrams (state machine, architecture, flow, coverage map) of what spec, plan and tasks already say | One feature at a time |
| [Spec Diagram](https://github.com/Quratulain-bilal/spec-kit-diagram-) (Spec Kit extension) | Mermaid diagrams of workflow state and task dependencies | Shows the process, not the system |
| OpenSpec `/opsx:explore` | ASCII diagrams in the conversation | Lost unless someone writes them into a file |
| OpenSpec `config.yaml` rules | Can require diagrams in an artifact; the docs' example is `design: Include sequence diagrams for complex flows` | Off unless you add the rule |

None of them describes the whole product. OpenSpec's living specs (`openspec/specs/`) record behavior, not structure, and Spec Kit keeps one spec per feature. None of them draws a change as a before/after of the system's structure, and nothing updates a diagram when a change is merged.

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
5. **Architecture diagrams, for the product and for each change.** One product diagram that is updated whenever a change merges, and one diagram per change that shows only what it adds, changes or removes compared with the product diagram.

"Shorter plans" alone is no longer a differentiator now that Superpowers PR #2333 has merged.

## OpenSpec in more depth

**How Lunch would plug in.** OpenSpec's official extension point is the custom schema ([docs/customization.md](https://github.com/Fission-AI/OpenSpec/blob/main/docs/customization.md)): a `schema.yaml` file plus templates in `openspec/schemas/<name>/`, created with `openspec schema init` or `fork`.
- The schema sets which documents a change produces, what each one depends on, and the instructions for writing it.
- `openspec/config.yaml` adds project context and rules for each document.
- Two recent additions help:
  - `skip_specs` (v1.7) lets a change skip specs when it doesn't alter behavior.
  - `openspec show --diff` (v1.11) prints all of a change's spec edits as one diff.

A `lunch` schema can therefore drop `design.md`, add a `review.md` for the reviewer, and set a length rule for each document, all without changing OpenSpec itself.

**Limits.**
- Lengths can only be suggested, not enforced:
  - The validator doesn't read custom schemas ([#829](https://github.com/Fission-AI/OpenSpec/issues/829)).
  - The 500-character requirement limit is only an info message ([#1976](https://github.com/Fission-AI/OpenSpec/issues/1976)).
- There are no gates that block a step ([#1142](https://github.com/Fission-AI/OpenSpec/issues/1142)).
- There's no schema registry ([#650](https://github.com/Fission-AI/OpenSpec/issues/650); a maintainer called it "on the roadmap, lower priority"). Schemas are shared by copying a folder.

**Ecosystem.** Every existing OpenSpec + Superpowers combination produces *more* documents than OpenSpec alone:
- The community [`superpowers-bridge` schema](https://github.com/JiangWay/openspec-schemas) (~225★) grows each change to 8 documents.
- [Comet](https://github.com/rpamis/comet) adds Superpowers design and plan files to OpenSpec's own. When it opens a PR it prints a short summary, but it doesn't save one for reviewers.

Other small projects:
- the [`anvil` schema](https://github.com/Fission-AI/OpenSpec/blob/main/docs/customization.md), which adds an adversarial review step;
- openspec-mcp;
- two VS Code viewers.

None of them writes a short summary for the reviewer. The closest prior work is a user's `openspec-refine` gist, posted in [#783](https://github.com/Fission-AI/OpenSpec/issues/783), which checks a change's documents for contradictions and duplication.

**Verbosity threads.**
- [#783](https://github.com/Fission-AI/OpenSpec/issues/783): decisions end up in the design doc but not in the specs, and the proposal contradicts the design. Still open.
- [Discussion #1152](https://github.com/Fission-AI/OpenSpec/discussions/1152): a proposed "review packet" for AI-written PRs. No replies.
- [Discussion #1159](https://github.com/Fission-AI/OpenSpec/discussions/1159): one comparison against plain Claude Code found OpenSpec produced 50% more code and cost 3× the API spend.
- The maintainers' [reviewing-changes doc](https://github.com/Fission-AI/OpenSpec/blob/main/docs/reviewing-changes.md) sets a "two-minute review" goal. There's no roadmap item on verbosity.

**Momentum** (from the GitHub API, 2026-09-30):

| | OpenSpec | Spec Kit |
|---|---|---|
| Stars | ~71k | ~140k |
| Contributors | ~138 | ~309 |
| Releases since July 1 | 11 (about weekly) | 51 (almost daily) |
| Community add-ons | 5 schemas | ~176 extensions |

Spec Kit is about twice the size and has a much larger add-on ecosystem.

## Direction

- **Base Lunch on OpenSpec.** Its delta specs are already the smallest unit a reviewer can read, and a custom schema can set exactly which documents a change produces. Spec Kit wins only on reach.
  - Trade-off: Bellhop runs on Spec Kit with the bridge, so choosing OpenSpec means either moving Bellhop over or running both workflows for a while.
- Ship Lunch as:
  - a `lunch` OpenSpec schema;
  - skills that bring in Superpowers' development habits;
  - a CI check that enforces document lengths, which OpenSpec itself won't.
- Make gaps 1–3 and 5 Lunch's own contribution.
- For gap 5, update the product diagram at the same step where OpenSpec's archive merges spec deltas into the living specs. Show the per-change diagram as a delta, marking what the change adds, changes and removes.
- Reuse or credit:
  - OpenSpec's added / modified / removed delta format;
  - cc-spex's `REVIEWERS.md` layout;
  - Kiro's "what must not change" section;
  - Marmelab's rule: no code in specs.
- Before committing to OpenSpec, try SpecKit Companion hands-on. It is the strongest reason to stay on Spec Kit.

## Decision point: mapping to Azure DevOps

Lunch's unit of work is a change, but ADO tracks Features, User Stories and Tasks. Tasks shouldn't become work items: they are implementation steps, change too often, and would duplicate the tasks document (gap 1).

- **Decide:** what a Lunch change corresponds to in ADO.
  - **Change = User Story.** The Feature is broken into stories (or the nearest equivalent, such as PBIs on a Scrum process), and each story gets one change. The change's tasks stay in its own document and never appear in ADO.
  - **Change = Feature.** A larger change is decomposed into stories, each becoming a work item and delivered as its own PR. The tasks document is per story.
- **Open:** whether the work item ID goes in the change's name or only in the PR, and whether Lunch creates stories itself or only links to existing ones.
