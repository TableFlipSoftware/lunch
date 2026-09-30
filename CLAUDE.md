# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Lunch is a collection of AI skills used to decompose, brainstorm, develop, and review code ("How do you eat the elephant? One bite at a time, over LUNCH."). It layers two toolkits:

- **Spec Kit** (specify → clarify → plan → tasks → implement) is the structure. It breaks a change into small pieces.
- **Superpowers** (brainstorming, TDD, subagent-driven development, code review) is the discipline. It sets how each piece gets built.

What Lunch adds on top is **documentation that makes changes easy to understand**. Every spec, plan, task list, and review note should be concise, and each fact should live in one place. A reader should be able to follow a change and see why it was made without reading every generated file.

## Guidance for work in this repo

- The documentation principle applies to this repo's own files and to the files its skills produce. Before adding text, check whether it's already written somewhere else. If it is, link to it.
- When a skill wraps a Spec Kit or Superpowers step, keep the upstream behavior and put Lunch's changes on top of it. Don't fork or restate the upstream content.

## Status

No skills, build system, or tests exist yet. Once they do, add the commands (including how to run a single test) and a high-level architecture overview here.
