# AGENTS.md

> Personal AI context template. Fill in the top two sections at project start. The rest is a stable rules framework.
> This file is read in full by AI — do not skip any section.
>
> This repo can be cloned directly into any project. AI tools auto-inject only files matching `AGENTS.md` / `CLAUDE.md` / `.cursorrules` by name — `experience/`, `README.md`, and other files are never auto-loaded. Physical isolation is unnecessary.

---

## ■ Identity (your role in this project)

<!-- Fill per project. Delete what doesn't apply. -->
- Role: (student dev / solo dev / backend engineer / full-stack / ...)
- Goal: What problem does this project solve?
- Skill level: (familiar / proficient / beginner) with the current stack

---

## ■ Project Overview (describe this project from scratch)

<!-- Refill for each new project so AI understands everything from zero. -->

- Project name:
- One-liner:
- Repository:
- Backend: (language + framework + version)
- Frontend: (framework + UI library + bundler)
- Database: (type + version)
- Deployment: (local / cloud server / Docker / ...)
- Server info: (IP / panel / SSH access. Write "local dev" if not applicable)

Current status:
- Done:
- In progress:
- TODO:

---

## ■ Skill Matrix

### Always Loaded
| Skill | Purpose |
|-------|---------|
| `caveman` | Compress communication, reduce token usage ~75% |

### Load on Demand
| Skill | Trigger |
|-------|---------|
| `frontend-design` | Creating pages, components, UI interactions |
| `ui-ux-pro-max` | Design discussion, UX flow, information architecture |
| `code-review` | Initial review, establishing review standards |
| `code-review-fix` | Auto-review after feature completion |
| `Git` | Branches, merges, conflict resolution, rebase |
| `caveman-commit` | Generating commit messages |
| `github` | PRs, Issues, CI operations |
| `self-improvement` | Command failure, user correction, new capability discovered |
| `find-skills` | Searching for new capability extensions |
| `skill-creator` | Solidifying repeatable workflows as skills |
| `cloudstudio-deploy` | Deploying static sites to cloud preview |

### Auto-Link Rules
- Feature complete → auto-load `code-review-fix`
- Generating commit → auto-use `caveman-commit`
- User correction or command failure → trigger `self-improvement`, write record to `experience/`
- Same operation repeated ≥3 times → ask whether to solidify via `skill-creator`

---

## ■ AI Interaction Rules

Applied across all projects.

### Communication
- Speak Chinese, concise and direct. No filler words.
- Technical decisions require rationale + numbers, not just steps.
- Provide copy-paste-ready scripts, SQL, configs. No screenshots.
- Present options with trade-offs before acting. Wait for confirmation.

### Boundaries
- SQL changes (DDL / DML): output first for approval. Never auto-execute.
- Never `git push` without explicit approval.
- Never connect to servers without explicit authorization.
- After feature completion: auto-run code review (duplication, exception handling, edge cases).

### Deliverables
- End each change session with a summary: what changed and why, itemized.
- Multi-file changes: explain the call chain between files.
- Before going live: run local build to confirm compilation passes.

---

## ■ Code Conventions (pick based on current stack)

<!-- Template sections. Keep what fits, delete what doesn't. -->

### Java / Spring Boot (if applicable)
- Entities use Lombok: `@Data`, `@NoArgsConstructor`, `@AllArgsConstructor`
- camelCase fields, snake_case DB columns (auto-mapped)
- Service layer: interface + impl (`XxxService` + `XxxServiceImpl`)
- Controller returns unified `Result<T>` (`code`, `message`, `data`)
- Exceptions handled globally via `@RestControllerAdvice`
- Time fields: `LocalDateTime`, serialized as `yyyy-MM-dd HH:mm:ss`
- Pagination: MyBatis-Plus `Page<T>`

### Vue3 / Element Plus (if applicable)
- Composition API + `<script setup>`
- Local state: `reactive`/`ref`; cross-component: Pinia
- API calls centralized in `api/` directory
- List pages must have loading state and empty-data hints
- Images: lazy-load via `v-lazy`

### SQL / Database (if applicable)
- Every table: `id` (auto-increment), `create_time`, `update_time`
- `update_time` with `ON UPDATE CURRENT_TIMESTAMP`
- Soft delete: `is_deleted` (tinyint, default 0). No physical deletes.
- Index high-frequency query fields and foreign keys.
- Every table and column must have `COMMENT`.

### Universal (all projects)
- Hardcoded strings/numbers → constants or enums
- Secrets (keys, passwords, tokens) → config file + env vars, excluded via `.gitignore`
- Logging: SLF4J. Disable SQL logs in production.

---

## ■ Git Workflow (all projects)

### Branches
```
main        ← stable, merge from develop only
develop     ← integration
feature/*   ← new features (e.g., feature/chat, feature/review)
fix/*       ← bug fixes
```

### Commit Format
```
<type>: <short description>
- change point 1
- change point 2
```
Types: `feat` / `fix` / `chore` / `perf` / `refactor`

### Steps
1. `git status` to check file states
2. `git add <files>` — exact targeting, no `git add .`
3. `git commit`
4. Wait for confirmation, then `git push`

### File State Reference
| State | Meaning | Action |
|-------|---------|--------|
| Untracked | New file, Git unaware | `git add` to track |
| Modified | Tracked file changed | `git add` to stage |
| Staged | Added, awaiting commit | `git commit` |

---

## ■ Experience Directory

For developer reference only. Safe to keep in project workspace: AI tools inject `AGENTS.md` by filename match; `experience/*.md` does not match any auto-load pattern.

```
experience/
├── pitfalls.md       ← Gotchas (scenario + cause + fix)
├── fixes.md          ← AI corrections (what was wrong → what's right)
├── optimization.md   ← Proven optimizations + data comparisons
├── decisions.md      ← Architecture Decision Records (why A over B)
└── habits.md         ← Personal dev habits and workflows
```

### AI Write Rules
- When `self-improvement` triggers: append record to the matching `experience/` file.
- After writing: tell the file name and entry summary.
- When detecting a pattern repeated ≥3 times: ask whether to document in `habits.md`.

---

## ■ Extension Notes

This file follows a "template + fill-in" design:
- Top two sections (Identity, Project Overview) → refill per project. Dynamic context.
- Middle/lower rules → stable across projects. Only change when a better practice is found.
- Experience → see `experience/`. Developer-only, never mixed into AI context.

When rules exceed 500 lines or a second tech stack is introduced:
- Split stack-specific rules into `profiles/` directory.
- Add a hard directive in this section requiring AI to read ALL profiles.
