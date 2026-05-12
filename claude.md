# CLAUDE.md — Project Instructions

> This file is read automatically by Claude Code at the start of every session.
> Follow these instructions for all sessions unless explicitly overridden by the user.

---

## 1. First Steps — Every Session

Before writing any code, do the following in order:

1. Read `SPEC.md` in full if it exists
2. Read `CURRENT_STATE.md` in `/docs/` to understand the current state of the project
3. Confirm your understanding of the task with a one-sentence summary before starting
4. Identify which files will likely be touched — state them before touching them

---

## 2. Learning-First Principle

This project is a learning environment as much as a build environment.
These rules are non-negotiable:

- **Explain before you build.** Before writing any non-trivial code, briefly explain
  what you're about to do and why — the approach, the tradeoffs, any alternatives
  you considered and rejected.
- **Teach through comments.** Leave comments that explain *why* a decision was made,
  not just what the code does. A future reader (including the user) should understand
  the reasoning without asking.
- **Flag patterns explicitly.** When you use a design pattern (factory, singleton,
  observer, strategy, etc.), name it. Say "this is a factory pattern because..."
  Don't let patterns be invisible.
- **Surface tradeoffs.** If there are two reasonable ways to solve a problem, briefly
  mention both and explain why you chose one over the other.
- **Never optimize prematurely.** Write the clear, readable version first.
  Optimize only when there is a demonstrated need, and explain the optimization
  when you make it.

---

## 3. Code Quality Standards

These apply to every language and every project.

### Clarity
- Code should read like plain English where possible
- Prefer explicit over clever — no one-liners that require deciphering
- Every function should do exactly one thing
- If a comment is needed to explain *what* code does, rewrite the code
- Comments explain *why*, not *what*
- Aim for code that a junior developer could understand without asking questions

### Object-Oriented Principles
- Follow SOLID principles:
  - **S** — Single responsibility: one class, one job
  - **O** — Open/closed: open for extension, closed for modification
  - **L** — Liskov substitution: subclasses must be substitutable for their parent
  - **I** — Interface segregation: prefer small, focused interfaces over large ones
  - **D** — Dependency inversion: depend on abstractions, not concretions
- Prefer composition over inheritance
- Keep classes small and focused — if a class is doing more than one job, split it
- No business logic inside presentation/view layers
- Encapsulate what varies — if something is likely to change, hide it behind an interface

### No Spaghetti
- No deeply nested conditionals — refactor to guard clauses or extracted functions
- No functions longer than ~30 lines — if it's longer, it's doing too much
- No file longer than ~200 lines without a strong reason — state the reason in a comment
- Dependencies flow one direction — lower layers never import from higher layers
- Shared utilities live in a clearly named shared location (e.g. `/lib/`, `/utils/`,
  `/shared/`) — never buried inside a feature folder

### Naming
- Be descriptive and unambiguous
- Avoid abbreviations unless they are universally understood (e.g. `id`, `url`, `api`)
- Functions named for what they do: `fetchUserById`, not `getData`
- Booleans named for what they represent: `isLoading`, `hasError`, `canSubmit`
- Classes named for what they are: nouns, not verbs

---

## 4. Testability Standards

Write code that is easy to test from the start — not as an afterthought.

- Pure functions wherever possible — same input always produces same output,
  no side effects
- Side effects (I/O, network, database, filesystem) isolated to clearly named
  modules — never embedded inside business logic
- Dependencies injected, not hardcoded — this makes mocking trivial
- No global state unless absolutely necessary — if it exists, document it clearly
- When writing a new function or class, pause and consider: "how would I test this?"
  If the answer is complicated, the design needs to change
- Flag untestable patterns with a `// TESTABILITY NOTE:` comment explaining the issue

---

## 5. Documentation Standards

### Inline documentation
- Every public function, class, and method gets a docstring/JSDoc/docblock comment
  that explains: what it does, what parameters it expects, what it returns,
  and any notable edge cases or exceptions
- Complex algorithms get a plain-English explanation before the code
- Magic numbers and non-obvious constants get an explanation

### CURRENT_STATE.md — Source of Truth
There is a `CURRENT_STATE.md` file in the `/docs/` directory.
It is the single source of truth for the current state of the project.
Always read it before starting any session.

**When to update it** — at the end of every task, or any time a change affects:
- The data model or schema
- API endpoints or contracts
- Environment variables or configuration
- Deployment state
- Any completed milestone or phase

**How to update it:**
- Edit in place — do not append a history log or create dated entries
- It should always reflect right now, not a timeline of changes
- Be specific and concrete — not "schema was updated" but exactly what changed
- If something was removed, remove it from the doc too
- Keep it concise — it is a briefing document, not a narrative

**What does not belong in CURRENT_STATE.md:**
- Reasons why decisions were made (that lives in `SPEC.md`)
- Task lists or to-dos
- Anything speculative or in-progress — only confirmed, working state

---

## 6. Permission Gate — Ask Before Proceeding

**Stop and ask the user before making any of the following changes:**

- Adding a new dependency or package
- Modifying the folder or project structure
- Changing any data model, schema, or API contract
- Refactoring code that is already working
- Making a change that touches more than 3 files simultaneously
- Introducing a new pattern or architectural approach not already in use
- Anything that could cause a regression in working functionality
- Any change where you are not fully confident in the approach

**When asking, always provide:**

1. **What** — plain-English description of the proposed change
2. **Why** — the specific reason this change is necessary or beneficial
3. **Scope** — which files will be created, modified, or deleted
4. **Risk** — anything that could break or regress as a result
5. **Alternatives** — any other approaches considered and why you recommend this one

Do not proceed until the user explicitly approves.
"Looks good" or "go ahead" is sufficient approval.

---

## 7. Dependency Management

Before adding any new dependency:

1. Stop and flag it to the user
2. Explain what it is, what it solves, and why a native solution won't work
3. Check if anything already in the project solves the problem
4. State the license and any known risks
5. Wait for approval

The best dependency is often no dependency.
Solve problems in under 20 lines of native code before reaching for a package.

---

## 8. Git Discipline

- Do not run `git commit` or `git push` unless explicitly asked
- Do not create new branches unless explicitly asked
- Do suggest logical commit points when a discrete unit of work is complete
- Propose a clear, descriptive commit message at each commit point
- Commit messages follow this format:
  `type(scope): short description` — e.g. `feat(cities): add bulk population script`

---

## 9. Folder Structure

> Confirm the folder structure with the user before creating new directories.
> Do not create files outside the agreed structure without asking first.

Document the agreed structure here at the start of each project.
Leave this section blank in the base file and fill it in per project.

```
# Project-specific structure goes here
```

---

## 10. When You Are Unsure

- Do not guess at business logic — ask
- Do not guess at data schema — leave an `// ASSUMPTION:` comment with your reasoning
- Do not guess at intended behavior — leave a `// QUESTION:` comment and flag it
- A short clarifying question is always better than building the wrong thing
- If you are 80% confident, say so — do not present uncertain decisions as definitive

---

## 11. Project-Specific Additions

> Add project-specific rules below this line.
> Everything above is the generic base and should not be modified per project.
> Copy this file into each new project and extend section 11 only.

---