---

name: process-inbox
description: Organize Markdown source notes from the Signal Inbox into durable notes, route ambiguous notes for review, and archive successfully processed sources.
argument-hint: "[optional scope]"
user-invocable: true
disable-model-invocation: true
---

# Process Inbox

Process eligible `.md` files recursively under `00 Inbox/`, including `00 Inbox/Needs Review/`. Ignore all other file types.

If the user supplies a scope, such as a filename or “created today,” process only that scope. Otherwise process every eligible note.

Follow the repository-wide rules in `.github/copilot-instructions.md`.

## Destination Rules

Route each distinct piece of durable information to one primary destination:

* `10 Notes/` — ongoing topics, systems, initiatives, questions, actions, risks, and developments
* `20 Designs/` — updates to an existing technical design
* `30 Reference/` — stable knowledge reusable across multiple topics
* `40 Deadline/` — explicit time-bound deliverables

Prefer an existing note. Create a new note only when no existing note reasonably represents the subject and the subject is likely to remain useful.

Do not automatically create a technical design. Update an existing design only; design creation belongs to the technical-design workflow.

A source may update multiple destinations when it contains genuinely distinct subjects. Do not copy the same information into multiple notes.

If the exact intended file path is occupied by a genuinely different note, use `-1`, `-2`, and so on. Do not use a suffix to avoid evaluating an existing note.

## Process Each Source Independently

For each source note:

1. Skip it if it already contains a valid `## Signal Processing` section, unless the user explicitly requested reprocessing.
2. Resolve its source date using the first reliable value:

   * explicit date in the content;
   * frontmatter date;
   * filename date;
   * file creation date;
   * file modification date.
3. Identify durable information:

   * current or confirmed information;
   * attributed reported information;
   * explicit decisions;
   * explicit actions or commitments;
   * open questions;
   * explicit deadlines or follow-up dates;
   * ideas to explore;
   * meaningful developments;
   * reusable reference knowledge;
   * technical-design details;
   * supported risks or blockers.
4. Select all required destination notes.
5. Check each destination for equivalent existing information.
6. Prepare all changes before treating the source as successfully processed.
7. Update or create the destinations incrementally.
8. Add a wikilink to the final archived source under `## Sources` or beside the relevant timeline entry.
9. Complete the archive and processing-stamp workflow.

Do not preserve conversational filler or repeated information that adds no future value.

## Canonical Topic Notes

When creating or updating a note under `10 Notes/`, use only relevant sections:

* `## Current Understanding`
* `## Confirmed Information`
* `## Reported Information`
* `## Decisions`
* `## Open Questions`
* `## Things to Do`
* `## Deadlines and Follow-Ups`
* `## Ideas to Explore`
* `## Risks and Blockers`
* `## Conflicting Information`
* `## Timeline`
* `## Related Notes`
* `## Sources`

Do not create empty sections.

Keep `Current Understanding` concise and current. Put meaningful historical developments under:

```markdown
## Timeline

### YYYY-MM-DD

Concise development.

Source: [[90 Archive/Inbox/YYYY/MM/Source Note]]
```

Resolve an open question only when a source clearly answers it. When sources conflict, preserve both positions under `## Conflicting Information`.

## Deadlines

Create a deadline note only when both are known:

* an identifiable deliverable;
* an explicit or deterministically resolvable date.

Do not turn vague timing such as “soon,” “maybe next week,” or “high priority” into a deadline.

Use:

```text
40 Deadline/YYYY-MM-DD - Deliverable Name.md
```

With:

```yaml
---
type: deadline
due: YYYY-MM-DD
created: YYYY-MM-DD
---
```

Include only:

* `## Deliverable`
* `## Deadline`
* `## Context`
* `## Related Notes`
* `## Sources`

The deadline note is the canonical home of the due date. Related notes should link to it rather than duplicate its content.

## Needs Review

If processing would require a material assumption:

1. Do not apply the uncertain information to destination notes.
2. Move the source to `00 Inbox/Needs Review/`.
3. Append or update one section:

```markdown
---

## Signal Review Needed

Last attempted: YYYY-MM-DD

### Issue

Explain the ambiguity.

### Questions

- Ask only the questions needed to organize the note.

### Additional Context

Add clarification below this line.
```

Preserve anything the user writes under `Additional Context`.

On later runs, retry a review note only when its content changed, clarification was added, or existing vault context now resolves the ambiguity. Otherwise leave it unchanged and report it as still requiring review.

Remove `## Signal Review Needed` only after processing succeeds.

## Archive and Processing Stamp

After all destination writes for a source succeed:

1. Move the source to `90 Archive/Inbox/YYYY/MM/`.
2. Append:

```markdown
---

## Signal Processing

Processed: YYYY-MM-DD

Referenced in:

- [[Destination Path]]
```

3. List every note created or updated from the source.
4. Do not list notes that were only read.
5. Ensure every destination links back to the archived source.

Do not create more than one processing section.

Treat the source as one complete operation. If any required step fails, do not claim success or leave the source stamped as processed. Keep or restore it under `00 Inbox/` and report the partial state.

## Special Cases

* **Empty note:** skip it.
* **Already processed:** skip it unless reprocessing was explicitly requested.
* **Duplicate information:** do not duplicate the content; add the source link when useful, then archive and stamp it.
* **No durable destination:** move it to `Needs Review` and ask whether it should be archived without integration.
* **Unsupported file type:** ignore it.

## Final Report

Report concisely:

### Processed

For each source:

* destinations created;
* destinations updated;
* deadline created, if any;
* archive location.

### Needs Review

* source;
* ambiguity;
* questions added.

### Skipped

* source;
* reason.

### Failed

* source;
* failed step;
* partial changes, if any;
* remediation needed.

### Summary

* examined;
* processed;
* moved to review;
* skipped;
* failed;
* notes created;
* notes updated;
* deadlines created;
* sources archived.
