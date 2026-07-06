# Repository Guidelines

## Vault Purpose

This repository is an Obsidian vault intended to become a practical second brain: a trusted place to capture information, develop ideas, manage active work, and resurface useful knowledge.

Optimize for usefulness over taxonomy. Notes should be easy to capture quickly, easy to find later, and connected through readable links.

## Core Second-Brain Structure

Use a simple PARA-inspired layout plus evergreen notes:

- `inbox.md` for unprocessed thoughts, links, tasks, questions, and quick captures.
- `daily/` for chronological daily notes named `YYYY-MM-DD.md`.
- `projects/` for active outcomes with a clear finish line.
- `areas/` for ongoing responsibilities without a fixed end date.
- `resources/` for reference material, reading notes, topics, and external sources.
- `notes/` for evergreen notes: small, reusable ideas written in the user's own words.
- `maps/` for maps of content that organize related notes and entry points.
- `templates/` for reusable note templates.
- `assets/` for images, PDFs, screenshots, and other attachments.
- `archive/` for completed, inactive, or no-longer-current material.

Do not create every folder preemptively unless content needs it. Start with the smallest structure that supports the user's current workflow.

## Note Types

### Inbox

`inbox.md` is temporary. Use it as a landing pad, not permanent storage. During cleanup, move items into daily notes, projects, areas, resources, evergreen notes, or archive them.

Good inbox items are short and easy to process:

- an idea to expand later
- a task that needs a home
- a link to read
- a question to investigate
- a quote or excerpt with source information

### Daily Notes

Daily notes should be dated with `YYYY-MM-DD.md` and kept in `daily/`.

Use them for:

- events and observations
- quick capture during the day
- lightweight journaling
- meeting notes that do not yet deserve their own note
- daily tasks and follow-ups

Prefer linking from daily notes to stable notes when an idea becomes reusable.

### Projects

A project is an active effort with an intended outcome. Project notes belong in `projects/`.

Project notes should usually include:

- outcome
- status
- next actions
- related notes
- decisions
- open questions

When a project is complete or inactive, move it to `archive/` or mark it clearly as archived.

### Areas

Areas are ongoing responsibilities such as health, finances, career, relationships, learning, or home. Area notes belong in `areas/`.

Use area notes for standards, recurring reviews, maintenance lists, and links to related projects or resources.

### Resources

Resources are topic or reference notes. Use `resources/` for source-heavy material such as books, articles, courses, tools, and subject references.

When a resource produces a reusable insight, extract that insight into an evergreen note in `notes/` and link back to the source.

### Evergreen Notes

Evergreen notes belong in `notes/`. They should be atomic, clear, and written in the user's own words.

Prefer note titles that express a specific idea, for example:

- `attention-is-a-limited-resource.md`
- `projects-need-next-actions.md`
- `learning-requires-retrieval.md`

Evergreen notes should usually include links to related notes, source notes, or maps of content.

### Maps of Content

Maps belong in `maps/`. A map is an index or guide for a topic, project cluster, life area, or knowledge domain.

Use maps to organize related notes without forcing every note into deep folders. Prefer curated links with short context over exhaustive lists.

## Markdown and Obsidian Conventions

Use Obsidian-flavored Markdown where it adds value:

- Use `[[wikilinks]]` for internal vault links.
- Use `[text](url)` for external links.
- Use `![[asset.png]]` or `![[document.pdf]]` for embeds.
- Use callouts for important context, warnings, decisions, or questions.
- Use Markdown task checkboxes for actionable items: `- [ ]`.

Prefer concise headings and sentence-case section titles. Avoid decorative formatting that makes notes harder to maintain.

## Naming Conventions

- Use lowercase, hyphen-separated filenames for reusable notes: `reading-list.md`.
- Use dated filenames for daily notes: `2026-07-06.md`.
- Use descriptive names over vague names: `ai-reading-list.md` instead of `links.md`.
- Keep filenames stable once other notes link to them.
- Store large or binary files in `assets/`.

## Properties and Metadata

Use frontmatter only when it helps retrieval, filtering, or review. Keep properties consistent and sparse.

Common properties:

```yaml
---
title: Example note
created: 2026-07-06
tags:
  - second-brain
status: active
---
```

Useful `status` values include `active`, `waiting`, `paused`, `done`, and `archived`.

Do not add metadata fields that are not useful yet. Plain Markdown is preferred unless structured metadata has a clear purpose.

## Review Workflow

Support these recurring workflows when adding notes or templates:

- Capture quickly into `inbox.md` or today's daily note.
- Process inbox items into the right note type.
- Connect related notes with wikilinks.
- Extract reusable ideas from daily notes and resources into evergreen notes.
- Review active projects and areas regularly.
- Archive completed or stale material instead of deleting useful history.

## Build, Test, and Development Commands

No build system, package manager, or test runner is configured in this repository. There is currently no `package.json`, `Makefile`, `pyproject.toml`, or equivalent manifest.

Useful local checks:

- `git status --short` shows changed and untracked files.
- `find . -maxdepth 2 -type f | sort` lists current vault files.
- `rg "\[\[.*\]\]"` can help inspect internal links.

If code is introduced later, add the relevant setup, build, lint, and test commands here.

## Validation Guidelines

For Markdown-only changes:

- Verify headings, links, embeds, and callouts render correctly in Obsidian or a Markdown previewer.
- Check that new internal links use the intended note names.
- Keep attachments under `assets/`.
- Avoid creating duplicate notes for the same idea.

If scripts or application code are added, include tests near the code or under a dedicated `tests/` directory and document the test command in this file.

## Commit and Pull Request Guidelines

This repository has no established commit convention yet. Use short, imperative commit messages such as:

- `Add daily note template`
- `Create inbox note`
- `Organize project notes`

Pull requests should include a brief description, the reason for the change, and screenshots only when visual Obsidian settings or rendered note formatting are affected.

## Agent-Specific Instructions

- Do not overwrite user notes or Obsidian configuration without checking current file contents first.
- Preserve user wording and personal context unless the user asks for rewriting.
- Prefer small, additive changes over large reorganizations.
- Do not move or rename notes unless the user asks or the current structure clearly requires it.
- When reorganizing, preserve links and explain the mapping from old locations to new locations.
- Keep repository-wide guidance in this file current when structure, tooling, or conventions change.
