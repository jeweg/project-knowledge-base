# AI Project Template

A template for AI-assisted projects: a curated knowledge layer that
survives across chats. Copy this folder to start a new project workspace.

> Setup documentation. Once your `STATE.md` has been bootstrapped and you no
> longer need to refer to this file, delete it -- it is template scaffolding,
> not project content. The rest of this README explains the structure and how
> to work with it; the bootstrap skill will offer to delete this file once
> setup completes.

Developed and used in Cursor; designed to also work with Claude Code, OpenAI
Codex CLI, and any other agent tool that reads `AGENTS.md` or `CLAUDE.md` at
the workspace root (most modern ones do). Only Cursor is verified at present.
See "Tool compatibility" under Design Principles for adapting to a tool that
does not.


## The Problem This Solves

When working with AI on longer efforts -- code analysis, debugging, design
exploration, research -- understanding accumulates in chat sessions and scattered
markdown files. Chats may hit context limits and get abandoned. Files become redundant
or contradictory as understanding evolves. You lose the overview, feel the urge to
start from scratch, but are afraid of losing buried insights.

This template provides a structure that separates raw exploration from curated
understanding, so you can work messily without losing clarity.


## Core Concepts

There are two kinds of material in this workspace:

* Working files (`_working/`) -- the messy, temporal record of exploration.
  Chat dumps, notes, half-formed ideas, dead ends, session summaries, handoffs
  for future agents. These are expected to be redundant, contradictory, and
  incomplete. They are raw material. Their primary function is preserving
  knowledge across short-lived agent sessions; err on the side of dumping --
  lost knowledge costs more than a messy file. See "Knowledge persistence
  across sessions" under Design Principles for the rationale.

* The state document (`STATE.md`) -- your single, clean, current-state summary.
  This is what you would hand someone to get them up to speed. It is rewritten
  as understanding matures, not appended to. Stale information is overwritten,
  not preserved alongside new information. It always starts with a "Hot List"
  (max 5 bullets, each terse -- a headline plus pointers, not a status
  paragraph) of the most important facts and priorities right now, and each
  section heading carries a freshness marker like `(updated 2026-04-01)`.

The key discipline: working files flow into STATE.md when an aspect crystallizes,
and then they get archived. STATE.md is never a log -- it is always a snapshot of
"what I know right now." The Hot List at the top is the fastest way to re-orient
after a break.

For larger or longer-lived projects, the curated layer can extend with two
optional documents -- `IDENTITY.md` (what the project IS) and `VISION.md` (where
it is HEADING). They are introduced manually when a project earns them, not by
default. See "Beyond STATE.md" below.


## Setting Up a New Workspace

1. Copy this template folder to a new location.
2. Open it in your editor (Cursor, VS Code, or similar).
3. If this workspace analyzes an external codebase, add the paths to AGENTS.md
   (or mention them when you tell the AI about the project in step 4) so the AI
   can read the relevant code.
4. Start a chat. The AI will notice that STATE.md does not exist and offer to
   create one based on what you tell it about the project. The initial STATE.md
   will include a Hot List, a Purpose section, Open Questions, and Action Items
   as a minimum skeleton.
5. Delete this file (`README.md`). It is only needed during setup. (GitHub
   conventions made `README.md` the right name for the template repo's
   landing page; once you have copied the template into a project, the
   file's job is done.)


## Day-to-Day Workflow

### Exploring

Work in chats as usual. When the AI produces findings, the default for clean
operational content is to update STATE.md directly -- add to an existing section
or create a new one. This keeps the curated knowledge layer current as you go.

Use a working file in `_working/` when a finding is preliminary (you are still
exploring, the conclusion might change), when it is a session summary or
handoff for future agents, or when you need a staging area before synthesis.
Working files exist primarily to preserve knowledge across short-lived agent
sessions; err toward dumping when in doubt -- lost knowledge costs more than
a messy file. They are dated by convention (e.g.
`2026-03-09-memory-layout-notes.md`) so you can tell them apart later.

### Consolidating

If you have been using working files, consolidate when an aspect becomes clear --
you have figured something out, a question is answered, a decision is made:

* Tell the AI: "consolidate these working files into STATE.md" (name the files,
  or say "everything about topic X").
* The AI reads the working files, identifies what is new relative to STATE.md,
  rewrites the relevant section(s), and tells you which files are now absorbed.
* Move absorbed files to `_archive/`. Or delete them -- they have served their
  purpose. The AI keeps `_working/INDEX.md` in sync, dropping entries for files
  that have left `_working/`.

You do not need to consolidate everything at once. One aspect at a time is fine.
Aspects still in progress stay as working files until they mature.

### Starting Fresh (Without Actually Starting Fresh)

When the urge hits to reorganize from scratch, resist copying everything into a
new folder. Instead:

* Rewrite the sections of STATE.md that feel stale. This is "starting fresh"
  for those aspects.
* Archive the working files that fed those sections.
* Leave in-progress aspects untouched.

This gives you the psychological reset without the information loss.

### Auditing

After a break, or when STATE.md has grown and you are not sure it is all still
accurate, ask the AI to audit it ("audit state" or "review state" -- or
"audit identity" / "audit vision" if those exist). It will check for internal
contradictions, stale freshness dates, dead code references, and whether the
Hot List still matches reality. It reports what it finds without silently
rewriting -- you decide what to fix.

### When Context Runs Out in a Chat

Before abandoning a long chat:

* Ask the AI to summarize its key findings and open questions.
* Have it write that summary to a working file or directly update STATE.md.
* Start a new chat. The AI will pick up STATE.md and the project rules
  automatically -- no need to re-explain the project from scratch.

The AI is supposed to do this without being asked too -- when you signal you
are wrapping up, when context is filling, or when work has produced findings
that have not landed in STATE.md, the agent drops a `_working/` handoff file
on its own. If a session ends without one and you notice, ask for it.


## Beyond STATE.md: Identity and Vision

Most projects are well-served by `STATE.md` alone. As a project grows and its
worldview stabilises, two more curated documents become useful at the workspace
root:

* `IDENTITY.md` -- what the project IS. Purpose, architectural commitments,
  posture, the "no, you cannot do that" rules that guard against shortcuts.
  Slow-changing.
* `VISION.md` -- where the project is HEADING. Long-term capabilities, reframes,
  moon shots, ambitions that orient design without driving immediate work.
  Updated occasionally.

The three together form the knowledge layer, each with a distinct role and
update cadence: STATE every session, IDENTITY when the worldview shifts (rare),
VISION when reflection produces durable new ambitions (occasional).

### When to introduce them

`IDENTITY.md` becomes useful when:

* The STATE.md Hot List keeps growing past 5 bullets because architectural
  framing is bleeding into operational state.
* You catch yourself re-explaining the same Purpose / Design Summary sections
  to every new agent. That content has crystallised; lift it.
* Multiple agents work on the project in parallel and need a stable reference
  for "what this project is" that does not get edited every session.

`VISION.md` becomes useful when:

* Brainstorming or reflection sessions produce ambitions that fit neither
  STATE (operational) nor any single design doc (too narrow).
* The project has aspirations beyond the immediate roadmap that are worth
  preserving and would otherwise be forgotten as you cycle on day-to-day work.

If a project has IDENTITY but no VISION, that is fine. If a project has VISION
but no IDENTITY, that is a smell -- vision without grounded identity tends to
drift. Add IDENTITY first.

### How to introduce them

There is deliberately no bootstrap skill or template skeleton for these files.
Their internal structure is project-specific -- the sections that fit one
project's identity will not fit another's -- so a portable skeleton would
either prescribe wrong shapes or be so thin as to be useless. A bootstrap
skill would also create an invocation surface that nudges agents toward
creating these files prematurely, defeating the earned-over-time model.

The introduction is conversational. Tell the AI:

* "lift the architectural sections of STATE.md into a new IDENTITY.md", or
* "we have enough vision-shaped material in `_working/`; create VISION.md
  from it"

The AI extracts the relevant content, writes the new file with sections that
fit the project, leaves cross-references in STATE.md, and updates AGENTS.md
context if helpful. Each knowledge layer file should open with a short preamble
pointing at the others (whichever exist), so a reader landing on any one knows
where to find the rest. After the lift, re-examine the STATE.md Hot List -- it
usually shrinks back below the 5-bullet line because architectural framing is
no longer cluttering it.

Note on freshness markers: STATE.md uses per-section markers (one per heading)
because its sections are rewritten independently. IDENTITY.md and VISION.md
use a single top-level marker on the document title, because the worldview and
ambitions tend to evolve as a whole; bump the title's marker on any
substantive edit.


## What Goes Where

* Findings, answered questions, decisions --> STATE.md (rewrite sections, update
  freshness markers, re-examine the Hot List). This is the default destination.
* Architectural commitments, posture, "do not do this" rules (when IDENTITY.md
  exists) --> IDENTITY.md
* Long-term ambitions, reframes, moon shots (when VISION.md exists) --> VISION.md
* In-workspace project layout (run / build / test commands for `impl/`,
  `android/`, etc.) --> a `## Layout` section in STATE.md, or section in
  IDENTITY.md if it exists
* Preliminary exploration, raw notes, chat dumps, session summaries, handoffs
  for future agents --> `_working/`
* Keyword index of working files --> `_working/INDEX.md` (agents maintain this
  automatically when they create or update working files; it lets future agents
  find relevant material without reading everything)
* Consumed working files --> `_archive/` (the user moves them; the agent
  surfaces which are absorbed and updates the INDEX). Or just delete.
* Rules the AI should always follow --> `.cursor/rules/`
* External codebase paths and project-specific AI instructions (when the
  workspace analyzes code that lives elsewhere) --> AGENTS.md


## Relationship to Karpathy's "LLM Wiki" Pattern

Andrey Karpathy proposed (April 2026) an LLM-maintained wiki as a persistent
knowledge layer over raw source documents. His design and this template share the
same core conviction: stop reconstructing understanding from scratch every session,
and maintain a living knowledge artifact instead.

### What we share

* Persistent synthesis as the central artifact, not ephemeral chat.
* Raw sources kept separate from curated knowledge.
* A schema file (AGENTS.md) that governs how the LLM maintains the knowledge layer.
* Rewrite-in-place rather than append-only updates.
* Freshness tracking on sections.
* Proactive maintenance -- the agent flags staleness, contradictions, and drift.
* Plain markdown, inspectable and editable, version-controlled.

### Where we differ

* Karpathy uses a multi-page wiki with cross-linked entity, concept, and synthesis
  pages. We default to a single STATE.md, with optional IDENTITY.md and VISION.md
  as a fixed-size extension when a project's worldview and ambitions outgrow what
  STATE alone can hold. This avoids inter-page consistency problems and ontology
  drift at the cost of a natural ceiling on volume. Beyond three curated documents,
  the right move is to split into separate workspaces.
* Karpathy defines ingest as a first-class automated operation (new source arrives,
  LLM updates 10-15 pages). Our system is conversation-driven -- the human controls
  the pace. This trades systematic coverage for tighter editorial control, which
  matters when "sources" are live code analysis rather than static documents.
* We add a working-file layer (_working/) as a sanctioned messy staging area.
  Karpathy's design has no equivalent -- material goes straight into the wiki.
* We add a Hot List for rapid re-orientation. Karpathy has no equivalent.
* We add an explicit audit workflow (check contradictions, staleness, dead
  references). Karpathy's "lint" concept is similar but broader -- it also covers
  orphan pages and missing cross-links, which are multi-page wiki concerns.

### What we deliberately left out

* Formal page taxonomy (entity, concept, comparison pages) -- current LLMs already
  handle document granularity well without being told what page types exist.
  Imposing a taxonomy adds friction without solving a real problem at this scale.
* log.md as a changelog -- version control already provides history. A separate
  log file is maintenance overhead for information you rarely look at.
* Immutable/mutable document type distinction -- in practice the content itself
  signals what should and should not be rewritten (a meeting transcript vs. a
  synthesis). The formal distinction solves a problem that does not arise when a
  human controls the workflow.
* Multi-page wiki structure -- correct for large cross-domain knowledge bases,
  but trades the context-size problem for a harder context-selection problem
  (which of 500 pages need updating?). A single document eliminates update
  ambiguity entirely.
* Write-back from queries as an automatic workflow -- Karpathy says valuable
  answers should become wiki pages. Our agents are instructed to default to
  updating STATE.md with findings, which covers most of the same ground. The
  remaining gap (useful answers the user does not explicitly ask to save) could
  be addressed with a proactive suggestion, but has not caused problems in
  practice.

### If you outgrow this template

The natural evolution path if a single STATE.md becomes unwieldy:

* First, introduce IDENTITY.md and VISION.md as described in "Beyond STATE.md"
  above. This handles a deepening single project -- architectural identity and
  long-term ambitions get their own homes, and STATE.md returns to operational
  state only.
* If the workspace genuinely contains multiple projects, split into per-project
  STATE-<name>.md files (or per-project subdirectories with their own
  three-document knowledge layer). Add a top-level STATE.md that summarizes all
  projects (a few lines each). The agent reads the top-level state first, then
  loads the relevant project.

This gives bounded context per session without the multi-page consistency problem.
Beyond that, retrieval infrastructure (keyword search, semantic search) over the
curated knowledge layer becomes necessary regardless of organizational pattern.


## Design Principles

These explain why the template is shaped the way it is. Useful context for anyone
modifying or extending it.

### Structure over procedure

AGENTS.md tells the AI what the workspace looks like and what the authority rules
are, but not step-by-step how to perform every task. Current LLMs handle judgment
calls -- what to update, how to split a topic, what granularity to use -- well
enough that specifying procedures for these things adds friction without improving
results. If you find yourself wanting to add detailed procedural instructions,
consider whether the model already does the right thing without them.

### Bounded curated layer

The curated layer is bounded: STATE.md by default, with optional IDENTITY.md and
VISION.md as a fixed extension. Not a wiki. This eliminates the hardest problems
in multi-page systems: inter-page consistency, update ambiguity (which pages
need changing?), and ontology drift (page categories that blur over time). The
tradeoff is a natural ceiling on volume. One project per workspace, three
documents max in the curated layer. If it gets unwieldy, split into separate
workspaces. See "If you outgrow this template" for the next step beyond that.

The cap at three is deliberate. Two would be too few -- experience showed that
mixing operational state with architectural worldview in one document creates a
hot list that keeps growing past its limits and eventually obscures what is
actually hot. Four or more starts to recreate wiki-style consistency problems.
Three is the smallest split where each tier has a distinct role (operational,
binding, aspirational) and each has a distinct update cadence (continuous, rare,
occasional). Adding a fourth would require an equally clean role and cadence
distinction, which has not surfaced in practice.

### Knowledge persistence across sessions

Agent chats are typically ephemeral. They hit context limits, get abandoned,
and -- depending on the tool -- may not even live with the project files (some
tools store chat history on the host machine, so a project accessed from
multiple machines effectively starts each session from a blank slate). The
working-files layer (`_working/`) is the mechanism for getting knowledge out of
a chat and into the project before that happens, so understanding is never
trapped inside a single session.

This shifts the operational default. When an agent is unsure whether a finding
belongs in the curated layer, the right move is to drop a working file -- the
cost of a messy file that gets archived later is much smaller than the cost of
knowledge lost when the chat ends. The keyword index (`_working/INDEX.md`) is
what makes this work without future agents getting buried; every working file
lives behind a few keywords that future agents grep before reading anything.

Working files do not need to pass any durability test. Session summaries, debug
notes, ideas that may not pan out, and handoffs for future agents are all valid
even if they will be obsolete in a week. Anything worth not losing is worth a
working file.

### The AI is a maintainer, not a retriever

The template positions the AI's role as continuously maintaining a knowledge
artifact, not just answering questions from context. This is a deliberate framing
that affects behavior: agents default to updating STATE.md (or dropping a
working file when in doubt) rather than producing standalone answers that
evaporate when the chat ends.

### Tool compatibility

The core system is tool-agnostic. AGENTS.md is plain markdown that any LLM can
read. The tool-specific pieces are:

* `.cursor/rules/` -- Cursor auto-loads these into every chat. Other tools ignore
  them.
* `.cursor/skills/` -- Cursor's progressive disclosure system. The bootstrapping
  procedure lives here. Other tools reach it via the pointer in AGENTS.md.
* `CLAUDE.md` -- Claude reads this file by convention. It points to AGENTS.md.

To adapt this template to a different tool, add that tool's equivalent of
"always read AGENTS.md first" in whatever mechanism the tool provides.

### When to add skills vs. keep instructions in AGENTS.md

Instructions belong in AGENTS.md when they apply to most sessions and are short
enough that their context cost is negligible. Move something to a skill file when
it runs rarely (like bootstrapping -- once per project) and is long enough to
matter. A skill only saves context when the procedure behind it is substantially
larger than its description. Most knowledge-management workflows are judgment-based
and compress to a few lines, so they belong in AGENTS.md.

A specific case: STATE.md has a bootstrap skill (`bootstrap-workspace`) but
IDENTITY.md and VISION.md deliberately do not. STATE is universal and has rigid
structure -- a portable skeleton is meaningful. IDENTITY and VISION are introduced
selectively, with project-specific structure, so a skeleton would prescribe wrong
shapes. A skill would also create an invocation surface that nudges agents toward
creating these files prematurely, defeating the earned-over-time model. Their
introduction is conversational instead, with the rule documented in AGENTS.md.


## Tips

* Don't over-organize `_working/`. The whole point is that it is allowed to be
  messy. You will consolidate later.
* STATE.md sections do not need to be long. A few sentences per aspect is fine
  early on. They grow and get rewritten as understanding deepens.
* If you find yourself wanting multiple STATE.md files, that is a signal that
  you have multiple projects and should split into separate workspaces.
* Back up your workspace folder periodically. Cursor stores chat transcripts in
  your home directory (`%USERPROFILE%\.cursor\projects\`), not in the workspace.
  If you want to preserve chat history too, back up that location as well.
* The `_archive/` folder is optional. If you are comfortable deleting consumed
  working files, skip it. It exists for people who are not ready to let go yet.
* For meetings and interviews, keep the full transcript in `_archive/` and a
  shorter summary in `_working/`. The summary is what agents will find via the
  index and use day-to-day. The full transcript stays available in case you need
  to look up a specific quote, exact wording, or a detail the summary missed.
  This way nothing is lost, but the material agents actually work with stays
  compact and focused.
