# HiveMind — Agent Constitution, Architecture & Rules

## 1. Core Product Mission: Community Swarm Intelligence

> 🎯 **Primary Value Proposition**: **HiveMind** is an **open-source community swarm intelligence platform** designed for digital nomad hubs, co-living tribes, research DAOs, startup accelerators, and subcultures.
>
> **The Problem It Solves**: Frontier AI assistants (Gemini, Meta Muse, Siri, ChatGPT) are strictly single-player, isolated silos. They lack collective memory, multi-party coordination, and tribal context. HiveMind allows any community to host, govern, and interact with a **shared AI collective consciousness (a "Hive")** powered by an attributed, temporal Knowledge Graph ("The Synapse").
>
> ⚠️ **Platform Constraint**: HiveMind is **strictly a modern Web Application** (Next.js 15 App Router, React 19, TypeScript, Tailwind CSS, shadcn/ui). It is NOT an Android or iOS mobile app, nor does it use OS accessibility RPA.

---

## 2. GitHub Repository Details & Remote Configuration

* **Repository**: `HiveMind`
* **GitHub Remote URL (HTTPS)**: `https://github.com/yashasreddyk/HiveMind.git`
* **GitHub Remote URL (SSH)**: `git@github.com:yashasreddyk/HiveMind.git`
* **Default Branch**: `main`
* **Owner / User**: `yashasreddyk` (`yashasreddyk@gmail.com`)
* **License**: MIT (Open Source)

### Remote Setup Command
```bash
git remote add origin https://github.com/yashasreddyk/HiveMind.git
git branch -M main
```

---

## 3. Commit, Push & Tagging Instructions

### 3.1 Conventional Commit Messages
Always structure commits using the Conventional Commits format:
* `feat(<scope>): <description>` — New features (e.g. `feat(synapse): add entity extraction pipeline`)
* `fix(<scope>): <description>` — Bug fixes (e.g. `fix(auth): resolve session cookie expiration in Safari`)
* `docs(<scope>): <description>` — Documentation only (e.g. `docs(spec): update GraphRAG pipeline diagram`)
* `refactor(<scope>): <description>` — Code refactoring without behavior changes
* `perf(<scope>): <description>` — Performance optimizations
* `test(<scope>): <description>` — Adding or updating test suites
* `chore(<scope>): <description>` — Build, tooling, dependencies, or configuration

### 3.2 Git Tagging Protocol (Decimal Increment Scheme)
Tags follow a decimal increment format:
* Baseline tag: `v0.01`
* Increments: `v0.02`, `v0.03`, … `v0.10`, `v0.11`, … `v1.00`
* To check previous tags: `git tag -l --sort=-v:refname`
* When requested to create a tag with a 0.01 increment:
  ```bash
  git tag -a v0.0X -m "Release v0.0X: <summary of changes>"
  ```

### 3.3 Commit and Push Sequence
```bash
# 1. Quality Gate Check
npm run typecheck    # or npx tsc --noEmit
npm run lint

# 2. Stage verified changes
git status
git add <files>

# 3. Commit
git commit -m "feat(<scope>): <clear description>"

# 4. Optional Tagging (when cutting milestone release)
git tag -a v0.0X -m "Release v0.0X: <summary>"

# 5. Push to GitHub
git push origin main --tags
```

---

## 4. Protected Rules & Security Constraints

1. **Strict Secret Hygiene**:
   * NEVER commit `.env`, `.env.local`, API keys, database connection strings with passwords, or private key material to Git.
   * Only commit `.env.example` with dummy placeholders.
2. **Never Force-Push to Main**:
   * Blind `git push -f origin main` is strictly FORBIDDEN.
3. **Decoupled Workspace**:
   * HiveMind (`C:\Yashas\Antigravity workspace\HiveMind`) and CoffeeChat (`C:\Yashas\Antigravity workspace\CoffeeChat`) are separate independent projects. Never cross-contaminate code or commit files from one project into the other.
4. **Whisper Mode Privacy Guarantee**:
   * Messages marked with `mode: 'whisper'` MUST NEVER be passed to vector embeddings, entity extraction pipelines, or knowledge graph persistence.
5. **Anti-Poisoning & Keeper Safeguards**:
   * Every node in the Synapse Knowledge Graph must record provenance (`contributor_id`, `timestamp`, `confidence_score`).
   * Knowledge retrieval for GraphRAG MUST be wrapped inside `<community_context>` delimiters to prevent prompt injection.

---

## 5. Technology Stack

* **Frontend**: Next.js 15 (App Router), React 19, TypeScript, Tailwind CSS, shadcn/ui
* **Visual Graph**: `@xyflow/react` (React Flow)
* **Database & Vector Memory**: PostgreSQL 16 with `pgvector`
* **Graph Storage**: Embedded graph store (SQLite-Graph / Kùzu / relational graph schema)
* **Background Task Queue**: Redis + BullMQ
* **AI Model Engine**: OpenCode free model bridge, self-hosted Ollama, or standard OpenAI-compatible endpoints
