# IFJ26 Table Maker

A helper for designing the LL(1) table and the precedence table of the IFJ26 compiler. Not part of the compiler itself.

## Language

### The project and what it holds

**Part**:
One of the four designed pieces of a project: the definition, the grammar rules, the precedence table and the reduction rules. Drafts, diffs and adoption work part by part.
_Avoid_: Section, tab, component

**Export naming**:
The project's naming settings for C exports: the symbol name map and the nonterminal, terminal and precedence-terminal prefixes. Not a part; never in a draft.
_Avoid_: Names, C names, prefixes

**Simulation input**:
The saved input string an LL or precedence simulation runs on. Not a part; never in a draft.
_Avoid_: Test input, sim string

**Project**:
One named design: a grammar definition with its grammar rules, and a precedence table with its reduction rules.
_Avoid_: Document, file, workspace

**Definition**:
The declared nonterminals N, terminals T and start symbol S of the grammar G = (N, T, P, S).
_Avoid_: Properties, header

**Grammar rules**:
The productions P of the grammar, from which the LL table is computed.
_Avoid_: Rules (on its own), productions list, LL rules

**LL table**:
The LL(1) parsing table computed from the grammar rules. It is never edited directly; it changes only when the grammar rules or the definition change.
_Avoid_: Parse table, predict table

**Precedence table**:
The hand-designed operator-precedence relations (`<`, `=`, `>`) between precedence terminals and `$`.
_Avoid_: Prec matrix, expression table

**Reduction rules**:
The rules the precedence simulation reduces handles by. They are separate from the grammar rules.
_Avoid_: Rules (on its own), precedence rules, expression grammar

### Versions of a project

**Snapshot**:
A frozen copy of a project's or a draft's content at one moment, kept in its history. It is *auto* (periodic), *named* (saved by the user) or *safety* (taken before a restore or import).
_Avoid_: Backup (that means a copy of the whole database), version

**Draft**:
An editable copy of a project's parts, attached to that project and forked from it at a known base point. Agents write only into drafts, and the human may edit them too; a project can have several, each with its own label and its own snapshots. Adopting or discarding ends a draft, but its history stays with the project.

**Changes**:
What adopting a draft would do to its project: the draft's parts compared with the project's current parts.
_Avoid_: Diff (in prose), delta, patch
_Avoid_: Version, branch, fork, copy

**Adopt**:
To let chosen parts of a draft overwrite the same parts of its project, done by the human. Adopting ends the draft.
_Avoid_: Merge, accept, apply, overwrite

**Discard**:
To end a draft without touching its project.
_Avoid_: Reject, delete

### Who acts

**Agent**:
An AI client that reads projects, drafts and snapshots and writes drafts through the agent interface. It never changes a project's content, never creates projects and never adopts; it may discard a draft.
_Avoid_: Bot, assistant, AI
