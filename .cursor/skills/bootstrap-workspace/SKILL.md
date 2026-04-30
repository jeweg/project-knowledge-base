---
name: bootstrap-workspace
description: >-
  Bootstrap a new knowledge workspace by creating STATE.md and the working file
  index. Use when STATE.md does not exist, or when the user says bootstrap,
  initialize, or set up the workspace.
---

# Bootstrap Workspace

This skill runs once when a new workspace is created from the template.

## When to run

* STATE.md does not exist yet.
* The user explicitly asks to bootstrap or initialize the workspace.

## Steps

1. Ask the user what the project or investigation is about.
2. If `_working/` already contains files, offer to read them and incorporate
   their content into the initial STATE.md.
3. If `_working/INDEX.md` does not exist but `_working/` contains files, create
   the index by reading each file and generating its keyword entry.
4. Create STATE.md using the skeleton below. Fill in real content based on what
   the user told you -- do not leave placeholders. Add more sections as needed,
   but never remove these:

```
# <Project Name> -- Project State

## Hot List

* <up to 5 bullets: the most important facts and priorities right now>

## Purpose (updated YYYY-MM-DD)

<What this project is and why it exists. 1-3 paragraphs.>

## Open Questions (updated YYYY-MM-DD)

* <Things not yet understood or decided>

## Action Items (updated YYYY-MM-DD)

* <What to do next>
```

5. If a top-level `README.md` exists and its content is the AI workspace
   template's setup documentation (it opens with a "Setup documentation"
   banner and contains sections like "The Problem This Solves", "Core
   Concepts", "Setting Up a New Workspace"), suggest to the user that it
   can be deleted now that the workspace is set up. Do not delete a
   `README.md` whose content is project documentation.
6. If the user wants an LF-only repository, point them at
   `_template/line-endings.md` and offer to run
   `python _template/apply-lf-policy.py`.
   Do not apply the policy silently; `.gitattributes` and `.editorconfig`
   are project policy files, not public-template defaults.
