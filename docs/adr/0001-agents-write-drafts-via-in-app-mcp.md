# Agents write only drafts, through an MCP endpoint in the running app

AI agents get direct access to projects so they can read the tables, sets, problems and simulations, and propose changes. To keep the human's work intact, an agent never changes a project's content. It writes only into a **draft**: an editable copy attached to the project and forked at a recorded base point. The human reviews a draft as a diff against the current project and **adopts** it part by part (definition, grammar rules, precedence table, reduction rules), or discards it. The agent interface is an MCP endpoint served by the running app on the tailnet. It goes through the same project store as the UI, and tailnet membership is the only authentication.

## Considered Options

- **Agents write projects directly.** Rejected: one bad agent edit would land in the human's work, and only snapshots could undo it.
- **Agents work on a duplicate project.** Rejected: it loses the link to the original, so changes would have to be copied back by hand, and the project list fills with copies.
- **A stdio MCP server or CLI opening the SQLite file.** Rejected: it would be a second writer next to the running app, which bypasses the store's revision checks. It would also only work on the machine that has the database.
- **A per-agent token.** Deferred: the app is reachable only on the tailnet, and agents can write nothing but drafts, so a stray client can at worst create clutter.

## Consequences

- Drafts are persisted with their own snapshot history. Adopting or discarding *ends* a draft rather than deleting it. An ended draft gets a final snapshot and keeps its tab on the History page, marked adopted or discarded. Its snapshots become read-only, and restoring one creates a new draft. It goes away only with its project, or when the human deletes it by hand.
- Humans may edit drafts too, so conflicts are detected **per part** rather than per document. An open draft refreshes live when an agent changes it.
- Export naming and simulation inputs are not part of a draft. They always come from the project, and only the human changes them.
- Simulations exposed to agents are pure: they never write the simulation inputs.
- Adoption takes a project safety snapshot first. A part also changed in the project since the draft's base is flagged "changed on both sides" and is not adopted by default.
