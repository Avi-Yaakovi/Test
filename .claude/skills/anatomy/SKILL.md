---
name: anatomy
description: Map how a codebase is put together — folder layout, entry points, main modules and how they connect, data flow, dependencies, and where build/test/CI/deploy config lives. Use when asked for an overview, tour, map, structure or "anatomy" of a repo, or when onboarding onto an unfamiliar codebase.
---

# Anatomy of a codebase

Produce a grounded map of the repository the user is working in. Every claim
should come from a file you actually read; cite it as `path/to/file:line`.
If something can't be determined from the code, say so instead of guessing.

## 0. Check there is something to map

- Run `git status` and `git log --oneline -5`, and list the files tracked in git (`git ls-files`).
- If the repo has no commits or no tracked files, say so plainly and stop.
- If the user named a subfolder or package, scope everything below to it.

## 1. Layout

- List the top-level folders and notable root files, and say what each is for.
- Identify the language(s), framework(s) and package manager from manifests
  (`package.json`, `pyproject.toml`, `requirements.txt`, `go.mod`, `Cargo.toml`,
  `pom.xml`, `*.csproj`, `Gemfile`, `composer.json`, etc.).
- Note whether it is a single app, a library, or a monorepo; for a monorepo,
  list the packages/apps and how they depend on each other.
- Skip generated or vendored folders (`node_modules`, `dist`, `build`, `.venv`,
  `vendor`, lockfiles) beyond a one-line mention.

## 2. Entry points

Find where execution starts, for example:
- `main` functions, `index.*` / `app.*` / `server.*` files, `bin` scripts
- `scripts` in `package.json`, console scripts in `pyproject.toml`, `Makefile` targets
- HTTP route definitions, CLI command registrations, background jobs, cron/scheduled tasks, serverless handlers
- For a front-end or single-file app: the HTML entry and the main script it loads

## 3. Main modules and how they connect

- Name the handful of modules/components that do the real work, one line each.
- Describe how they call each other: which layer talks to which
  (e.g. routes → services → data access), shared utilities, state management.
- Follow one representative request or user action end to end and show the
  path through the code with `file:line` references.

## 4. Data and external systems

- Where data lives: databases, ORMs/schemas, migrations, local storage, files.
- External services and APIs the code calls, and where their clients are configured.
- How configuration and secrets are supplied (env vars, config files) — name
  the variables, never print secret values.

## 5. Build, test, CI, deploy

- How to install, run locally, build and test (commands from the manifests/README).
- Test layout and framework; roughly how much of the code is covered by tests.
- CI workflows (`.github/workflows`, etc.) and what they run.
- Deploy setup (Dockerfiles, `vercel.json`, `netlify.toml`, IaC, deploy scripts).

## 6. Observations

Briefly flag anything a newcomer should know: surprising structure, dead or
duplicated code, missing tests, TODO hot spots, outdated docs. Keep it to
facts you saw, not general advice.

## Working method

- For a small repo, read files directly. For a large one, sweep with search
  first (or delegate broad searches to an Explore agent) and read only what
  the map needs.
- Prefer reading manifests, entry files and route/config definitions over
  reading every file.

## Output format

Write the report in this order, with short sections and bullet points:

1. **Summary** — 2–3 sentences: what the project is and how it's built.
2. **Layout** — a compact tree of the important folders with one-line notes.
3. **Entry points**
4. **Main modules & data flow** — include the traced request/action.
5. **Data & external systems**
6. **Build / test / CI / deploy** — the exact commands.
7. **Observations**

Use `path:line` references throughout. If the user asks for something they can
share, offer to turn the report into a page or document.
