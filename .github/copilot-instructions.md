# Copilot instructions for Signal

This repository is a personal knowledge-management vault built around Obsidian-style Markdown notes rather than a traditional application. Most meaningful work is organizing, linking, and preserving notes in a consistent structure.

## Repository shape

- The main content is organized by purpose:
  - `00 Inbox/` for incoming notes
  - `10 Notes/` for canonical topic notes
  - `20 Designs/` for design documents
  - `30 Reference/` for reusable reference material
  - `40 Deadlines/` for explicit time-bound deliverables
  - `90 Archive/` for processed notes
  - `95 Assets/` for attachments
  - `99 _System/` for system and utility files
  - `temp/` for temporary processing notes
- `.obsidian/` contains Obsidian configuration. Preserve its settings unless you are explicitly changing them.

## Build, test, and lint

No build, test, or lint commands are defined for this repository. If you are editing only notes/content, validate by checking that files are in the correct folders, Markdown remains intact, and any links or references are consistent.

## Inbox-processing workflow

The authoritative workflow for processing inbox notes is `temp/Process Inbox.md`. When you work with notes under `00 Inbox/`:

- Preserve the original source content. Do not rewrite, summarize, or delete it.
- Prefer updating an existing canonical note in `10 Notes/`, `20 Designs/`, `30 Reference/`, or `40 Deadline/` instead of creating a new note.
- Use Obsidian wikilinks such as `[[10 Notes/Topic]]`; do not include the `.md` extension.
- Add a source link back to the archived note from each destination note that was updated.
- If the information is ambiguous or requires unsupported assumptions, move the note to `00 Inbox/Needs Review/` and add a clear review request instead of guessing.
- After successful processing, archive the source note under `90 Archive/Inbox/YYYY/MM/` and add a processing stamp.

## Writing and organization conventions

- Keep content in Markdown.
- Do not invent facts, deadlines, ownership, or status. Only record information that is supported by the source note or an existing canonical note.
- Preserve uncertainty and conflicts rather than resolving them through assumptions.
- Keep `## Current Understanding` concise and place historical developments in a `## Timeline` section.
- Avoid duplicate information; link to an existing note when the same concept is already covered.
- Prefer durable, reusable notes over temporary or catch-all notes.

## Notes for future Copilot sessions

- Treat this repository as a content vault first and a codebase second.
- When making changes, favor small, targeted updates that fit the existing folder taxonomy and note conventions.
- If a task is unclear, look for an existing note that already covers the subject before creating a new one.
