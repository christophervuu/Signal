# Process Inbox

Process every Markdown file (`.md`) located recursively under the `00 Inbox/` folder, including files under `00 Inbox/Needs Review/`.

Ignore files with any other extension.

For each eligible source note, organize its useful information into the most appropriate durable Markdown notes within the Signal vault.

Possible destination folders are:

* `10 Notes/` for canonical topic notes and ongoing context
* `20 Designs/` for existing technical-design documents when the source contains relevant design information
* `30 Reference/` for stable, reusable information that applies beyond one topic or deliverable
* `40 Deadlines/` for explicit time-bound deliverables

Prefer updating an existing destination note over creating a new one.

Preserve the original source content. After processing succeeds completely, move the source note to the Inbox archive and append a processing stamp showing every durable note that was created or updated from that source.

---

## Operating Rules

### 1. Preserve source content

Do not delete, rewrite, summarize, correct, reorder, or remove any original content from a source note.

The only permitted additions to a source note are:

* a `## Signal Review Needed` section when the note cannot be processed safely; or
* a `## Signal Processing` section after the note has been processed successfully.

Any clarification manually added by the user must also be preserved.

---

### 2. Prefer existing canonical notes

Before creating a new note, search the appropriate destination folders for an existing note that reasonably represents the same topic, design, reference subject, or deliverable.

Update an existing note when it represents the same subject.

Do not create new notes merely because:

* the wording differs;
* a synonym is used;
* the source focuses on a temporary aspect of an existing topic;
* the existing note is in another subfolder;
* the preferred filename is already occupied.

---

### 3. Create durable notes only when justified

Create a new canonical topic note only when:

* no existing note reasonably represents the subject;
* the subject is meaningful enough to preserve;
* the subject is likely to receive more information or remain useful later.

Do not create vague or catch-all notes such as:

* `Miscellaneous`
* `Random Thoughts`
* `Meeting Notes`
* `Follow Ups`
* `General Information`

A source note does not need to create a new durable note merely to be considered processed.

---

### 4. Handle multiple subjects without duplicating information

A single source note may update multiple destination notes when it contains distinct information about meaningfully different subjects.

Give each distinct piece of information one primary canonical destination.

Do not copy the same information into several destination notes.

When information is relevant to another note, add an Obsidian wikilink to the primary canonical note rather than duplicating the full information.

Example:

* Carrier V2 validation information belongs primarily in the Carrier V2 note.
* A separate environment-visibility idea may belong in a Deployment Visibility note.
* The Carrier V2 note and Deployment Visibility note may link to each other when useful.

---

### 5. Use Obsidian wikilinks

Link to Markdown notes using Obsidian wikilinks.

Use the vault-relative folder path and filename without the `.md` extension.

Example:

```markdown
[[10 Notes/Carrier V2]]
```

Example design link:

```markdown
[[20 Designs/Carrier V2 Shipment Integration]]
```

Example source link:

```markdown
[[90 Archive/Inbox/2026/07/2026-07-06 Carrier V2 discussion]]
```

Do not include the `.md` extension.

Incorrect:

```markdown
[[10 Notes/Carrier V2.md]]
```

Use the final resolved path in every wikilink.

---

### 6. Handle filename collisions

Before creating a new file whose intended path already exists:

1. Determine whether the existing file is the correct canonical destination.
2. Update the existing file when it represents the same subject.
3. Create a separate file only when it represents a genuinely different subject.

If a genuinely separate note would otherwise use an occupied path, append a numeric suffix:

```text
Topic Name-1.md
Topic Name-2.md
```

Do not use a numeric suffix merely to avoid evaluating whether the existing note should be updated.

---

### 7. Do not invent information

Do not invent or assume:

* facts;
* decisions;
* owners;
* deadlines;
* commitments;
* completion states;
* causes;
* requirements;
* relationships between events;
* priority;
* delivery status.

Include information only when it is directly supported by:

* the source note; or
* an existing destination note being updated.

---

### 8. Preserve the source’s certainty

Do not increase the certainty of the original wording.

Examples:

* “James confirmed” may be recorded as information reported by James.
* “James thinks” must not become a confirmed fact.
* “We should consider” must not become a decision or commitment.
* “Maybe next week” must not become a deadline.
* “This might block the release” must not become “The release is blocked.”

Attribute reported information when the source identifies the person or group.

---

### 9. Allow grounded synthesis

You may summarize, classify, combine, and reorganize information that is directly supported by the source.

You may form a concise synthesis when it logically follows from the available facts.

Example:

Source information:

* QA validation is incomplete.
* Production readiness depends on QA validation.

Acceptable synthesis:

> Production readiness remains unresolved because QA validation is incomplete.

Unacceptable synthesis:

> The production deployment will be delayed.

Do not introduce predictions or unsupported conclusions.

---

### 10. Preserve ambiguity and conflict

When information is incomplete, ambiguous, uncertain, or conflicting:

* do not resolve it through assumption;
* preserve the uncertainty;
* use `Open Questions`, `Reported Information`, or `Conflicting Information`, as appropriate.

When two sources conflict, record both positions and state that the current answer remains unresolved.

Example:

```markdown
## Conflicting Information

- James reported that validation may require another week.
- A later release note stated that validation was expected to finish Wednesday.
- The current completion date remains unconfirmed.
```

---

### 11. Extract only durable or actionable information

Useful information may include:

* current understanding;
* confirmed information;
* reported information;
* explicit decisions;
* explicit actions or commitments;
* open questions;
* explicit deadlines;
* promised follow-ups;
* ideas worth exploring;
* meaningful developments;
* stable reusable knowledge;
* technical-design details;
* risks or blockers explicitly supported by the source.

Do not preserve conversational filler or repeated information that adds no useful context.

---

### 12. Do not use external systems

Do not query or modify:

* Azure DevOps;
* email;
* calendar;
* GitHub;
* messaging systems;
* external websites;
* any other external service.

This command organizes only the information already available within the Signal vault.

---

### 13. Update incrementally

Preserve useful existing content in destination notes.

Do not replace an entire destination note unless restructuring is necessary to remove duplication or restore clarity.

Before adding information:

* check whether the same meaning is already present;
* update an existing statement when the new source materially changes it;
* avoid adding repeated timeline entries;
* preserve meaningful historical information.

---

### 14. Omit empty sections

Do not add headings with no supporting content.

Use only the sections needed for the information being organized.

---

## Source Date Resolution

Determine the source date using the first reliable value available in this order:

1. An explicit date stated in the note.
2. A date property in frontmatter.
3. A date contained in the filename.
4. The file creation date.
5. The file modification date.

Use the resolved source date for timeline entries and archive placement.

Do not infer a date when none can be determined reliably.

---

## Destination Selection

For each distinct piece of useful information, choose the best destination.

### `10 Notes/`

Use for:

* ongoing topics;
* projects or initiatives;
* systems;
* recurring operational concerns;
* people-related context when durable;
* current understanding;
* questions, actions, and developments related to a topic.

### `20 Designs/`

Update an existing design when the source contains information directly relevant to:

* system behavior;
* technical requirements;
* architecture;
* interfaces or contracts;
* failure handling;
* observability;
* deployment;
* security;
* design decisions;
* design risks or questions.

Do not automatically create a full technical design from an Inbox note.

Create or substantially restructure a design only when explicitly requested through the technical-design workflow.

### `30 Reference/`

Use for stable, reusable information such as:

* integration patterns;
* system descriptions;
* standard processes;
* technical standards;
* terminology;
* guidance that applies to multiple work items.

Do not place temporary project status or one-time conversation details in Reference.

### `40 Deadlines/`

Use only for explicit, time-bound deliverables.

---

## Canonical Topic Note Structure

Canonical notes under `10 Notes/` may use the following sections when relevant:

```markdown
# Topic Name

## Current Understanding

A concise synthesis of what is currently known.

## Confirmed Information

Facts directly established by available sources.

## Reported Information

Claims, opinions, expectations, or updates attributed to a person or group.

## Decisions

Only decisions explicitly confirmed by a source.

## Open Questions

Unresolved questions.

## Things to Do

Only explicit follow-ups or commitments supported by a source.

## Deadlines and Follow-Ups

Links to related deadline notes and any timing information that does not justify a separate deadline note.

## Ideas to Explore

Possibilities or investigations that are not commitments.

## Risks and Blockers

Only risks or blockers directly supported by the source.

## Conflicting Information

Conflicting claims or unresolved contradictions.

## Timeline

### YYYY-MM-DD

A concise description of a meaningful development.

## Related Notes

Links to relevant canonical notes, designs, references, or deadlines.

## Sources

Links to archived source notes.
```

Do not add every section automatically.

---

## Updating Current Understanding

Keep `## Current Understanding` concise and current.

Use it to explain the latest synthesized state, not to preserve the full history.

Place historical developments under `## Timeline`.

When new information changes the current understanding:

* revise the current summary;
* preserve the meaningful change in the timeline;
* do not retain obsolete statements as though they are still current.

---

## Timeline Rules

Add a timeline entry when the source represents a meaningful development.

Use:

```markdown
## Timeline

### YYYY-MM-DD

Concise description of the development.

Source: [[Archived Source Note]]
```

Do not create a timeline entry for:

* repeated information;
* conversational filler;
* formatting changes;
* information already represented by an equivalent entry.

---

## Source-Link Rules

Every durable note created or updated from a source must contain a link back to the archived source note.

Add the source link under `## Sources`, or include it directly with the relevant timeline entry when more precise attribution is useful.

Avoid adding the same source link more than once within the same destination note.

---

## Deadline Rules

Create a deadline note only when:

* there is an identifiable deliverable; and
* the source provides an explicit or deterministically resolvable deadline.

Examples that qualify:

* “The design is due July 10.”
* “Have the release plan ready by Friday,” when the source date makes the Friday unambiguous.
* “Follow up two weeks from today,” when the source date is reliable.

Examples that do not qualify:

* “We should do this soon.”
* “Maybe next week.”
* “This is high priority.”
* “We need this eventually.”

When timing is vague, retain it as reported information or an open question in the related canonical note.

### Deadline filename

Name deadline files using:

```text
YYYY-MM-DD - Deliverable Name.md
```

Example:

```text
2026-07-10 - Carrier V2 technical design review.md
```

### Deadline frontmatter

Use:

```yaml
---
type: deadline
due: YYYY-MM-DD
created: YYYY-MM-DD
---
```

### Deadline note structure

```markdown
# Deliverable Name

## Deliverable

Describe the required result.

## Deadline

State the deadline exactly as resolved.

## Context

Provide concise context explaining why the deliverable exists.

## Related Notes

- [[Related Topic Note]]
- [[Related Design Note]]

## Sources

- [[Archived Source Note]]
```

Do not duplicate the full topic or design inside the deadline note.

The deadline note is the canonical location for the due date. Related notes should link to it.

---

## Needs Review Workflow

If a source note cannot be organized without making a material assumption:

1. Do not update any destination notes from uncertain information.

2. Move the source note to:

   `00 Inbox/Needs Review/`

3. Append one `## Signal Review Needed` section.

4. Explain exactly what is ambiguous.

5. Ask specific questions that would make the note processable.

6. Provide an `### Additional Context` section for the user.

Use this format:

```markdown
---

## Signal Review Needed

Last attempted: YYYY-MM-DD

Signal could not organize this note without making an unsupported assumption.

### Issue

Concise explanation of what is ambiguous.

### Questions

- Specific question needed to determine the correct destination or meaning.
- Additional specific question when necessary.

### Additional Context

Add clarification below this line.
```

Do not append more than one `## Signal Review Needed` section.

If the section already exists:

* update `Last attempted`;
* revise the issue or questions only when necessary;
* preserve all user-added content under `### Additional Context`.

---

## Reprocessing Needs Review Notes

Every Process Inbox run must inspect `.md` files recursively under:

* `00 Inbox/`; and
* `00 Inbox/Needs Review/`.

Reattempt a note under `Needs Review` when:

* the source content changed;
* the user added clarification;
* relevant canonical notes now provide enough context;
* the previous ambiguity can now be resolved safely.

If no useful new information is available:

* leave the note under `Needs Review`;
* do not append duplicate questions;
* report it as still requiring review.

When processing later succeeds:

* preserve the original content;
* preserve the user’s additional context;
* remove the obsolete `## Signal Review Needed` section;
* complete the normal archive and processing-stamp workflow.

Do not archive or stamp a note as processed until processing succeeds completely.

---

## Successfully Processing a Source Note

Treat each source note as one complete operation.

The successful sequence is:

1. Read and interpret the source.

2. Determine every required destination.

3. Prepare all destination updates.

4. Update or create every destination successfully.

5. Resolve any filename collisions.

6. Move the source note to:

   `90 Archive/Inbox/YYYY/MM/`

7. Append the `## Signal Processing` section to the archived source note.

8. Add links from every destination note back to the archived source.

9. Confirm that all files exist in their expected final locations.

If any required step fails:

* do not mark the source as successfully processed;
* do not append a `## Signal Processing` section;
* do not leave the source archived as though processing completed;
* return or keep the source under `00 Inbox/`;
* report the failure clearly.

---

## Processing Stamp

After processing succeeds and the source has been moved to the archive, append this section to the bottom of the archived source note:

```markdown
---

## Signal Processing

Processed: YYYY-MM-DD

Referenced in:

- [[Destination Note Path]]
```

Example:

```markdown
---

## Signal Processing

Processed: 2026-07-06

Referenced in:

- [[10 Notes/Carrier V2]]
- [[20 Designs/Carrier V2 Shipment Integration]]
- [[40 Deadlines/2026-07-10 - Carrier V2 technical design review]]
```

The `Referenced in` list must contain every durable note created or updated from the source.

Do not add a destination that was merely read but not changed.

Do not add more than one `## Signal Processing` section.

If a processing section already exists, update the existing section instead of appending a duplicate.

---

## Previously Processed Notes

A source note that already contains a valid `## Signal Processing` section is considered processed.

Do not process it again unless:

* it has been manually returned to `00 Inbox/`; or
* the user explicitly requests reprocessing.

If explicitly reprocessed:

* preserve the existing processing history;
* update the existing processing section;
* avoid duplicating information in destination notes.

---

## Notes With No Durable Information

Do not create a canonical note merely to dispose of an Inbox item.

Handle these cases as follows:

### Empty note

Skip it and report it under `Skipped`.

### Duplicate information

If the note contains only information already represented in a canonical note:

* add the source link to the appropriate canonical note when useful;
* archive and stamp the source;
* do not duplicate the existing information.

### Temporary or disposable information

If the note contains no durable information and its intent is clear:

* leave it under `00 Inbox/Needs Review/`;
* explain that no durable destination was identified;
* ask whether it should be archived without integration or discarded manually.

Do not delete it automatically.

### Ambiguous information

Move it to `00 Inbox/Needs Review/` and request clarification.

---

## Final Report

After the run completes, provide a concise report.

### Processed

For each successfully processed source note, report:

* source note;
* destination notes created;
* destination notes updated;
* deadline notes created;
* archive destination.

### Needs Review

For each note requiring clarification, report:

* source note;
* reason it could not be processed;
* questions added.

### Skipped

Report notes that were:

* empty;
* already processed;
* unchanged under `Needs Review`;
* unsupported file types.

### Failed

For each failed note, report:

* source note;
* step that failed;
* whether any destination files were changed;
* remediation needed.

### Summary

Report:

* number of Markdown source notes examined;
* number successfully processed;
* number moved to Needs Review;
* number skipped;
* number failed;
* number of canonical notes created;
* number of canonical notes updated;
* number of design notes updated;
* number of reference notes created or updated;
* number of deadline notes created;
* number of source notes archived.
