# Lunch

AI skills used to decompose, brainstorm, develop, and review code.

> How do you eat the elephant? One bite at a time, over LUNCH.

## The idea

Lunch layers two existing toolkits:

- **[Spec Kit](https://github.com/github/spec-kit)** provides the structure: a spec-driven flow (specify → clarify → plan → tasks → implement) that breaks a large change into small, reviewable pieces.
- **[Superpowers](https://github.com/obra/superpowers)** provides the discipline: skills for brainstorming, test-driven development, subagent-driven execution, and code review that set how each piece gets built.

Spec Kit decides *what* the bites are. Superpowers decides *how* each bite gets eaten.

## What Lunch adds

The goal is to make changes easier to understand. Both toolkits produce a lot of documents, including specs, plans, task lists, and review notes. These are often long, repeat each other, and are hard to skim. Lunch focuses on documentation that is:

- **Concise:** each artifact says what a reader needs to know and stops.
- **Non-redundant:** a fact lives in one place and is linked from everywhere else.
- **Reviewable:** a person should be able to understand a change, and why it was made, without reading every generated file.

## Status

Early. The repository doesn't contain any skills yet.

## License

MIT. See [LICENSE](LICENSE).
