# 🧠 HiveMind

> **Open-Source Community Swarm Intelligence Platform**  
> Turn your community, nomad tribe, or research group into a living, communal AI consciousness.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![Next.js 15](https://img.shields.io/badge/Next.js-15-black)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue)](https://www.typescriptlang.org/)

---

## 🌟 What is HiveMind?

Current frontier AI assistants (**Google Gemini, Meta Muse, Apple Intelligence, ChatGPT**) are strictly **single-player, solitary bubbles**. Each user operates in complete isolation with zero collective memory or multi-party coordination.

**HiveMind flips this paradigm on its head.**

HiveMind is a self-hostable, open-source web application that allows any community, co-living space, DAO, nomad tribe, or startup incubator to host, govern, and interact with a **shared AI collective consciousness (a "Hive")**.

Instead of interacting with a generic assistant that knows nothing about your tribe, members connect to a **communal intelligence** whose memory, personality, and knowledge graph are continuously shaped, updated, and refined by the community itself.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                       THE HIVEMIND PARADIGM SHIFT                           │
├──────────────────────────────────────┬──────────────────────────────────────┤
│       LEGACY PERSONAL AI ASSISTANT   │          HIVEMIND COMMUNITY SWARM    │
├──────────────────────────────────────┼──────────────────────────────────────┤
│ • 1 User ↔ 1 Isolated AI             │ • 1 Community ↔ 1 Shared Collective  │
│ • Private, siloed memory             │ • Communal living knowledge graph    │
│ • Generic global personality         │ • Custom community vibe/constitution │
│ • Passive text output                │ • Autonomous group coordinator       │
│ • High API cost / Subscription       │ • Open source / Free OpenCode models │
└──────────────────────────────────────┴──────────────────────────────────────┘
```

---

## 🚀 Key Features

### 1. 🐝 The Hive (Community Container)
* Host multiple distinct communities with custom constitutions, vibes, and access control.
* **Access Gating**: Public, Invite-only, Quiz/Application vetting, or Domain-gated (`@university.edu`).

### 2. ⚡ The Synapse (Attributed Knowledge Graph)
* Rather than a flat text vector database, the Synapse maintains an attributed, temporal Knowledge Graph of entities, relations, and claims.
* Every memory node tracks **who stated it**, **when**, and its **confidence level** (`provisional` $\to$ `corroborated` $\to$ `canon`).

### 3. 🤫 Dual Thought Modes (Privacy Architecture)
* **Whisper Mode (Private 1-on-1)**: Ask sensitive questions without your queries or answers entering the shared knowledge graph.
* **Synapse Mode (Public / Collective)**: Discussions and insights are analyzed by the memory synthesis worker and woven into the collective brain.

### 4. 🛡️ Anti-Poisoning & Keeper Governance
* Community creators and appointed moderators have a **Keeper Dashboard** to inspect newly formed knowledge graph relations, flag false claims, or purge memories with one click.
* All memory ingestion is isolated within strict `<community_context>` prompt injection firewalls.

### 5. 🗺️ Interactive Mind Map Visualizer
* An interactive 2D/3D force-directed graph (powered by React Flow) allowing community members to visually explore what their HiveMind knows in real time.

### 6. ☕ Gathering & Meetup Coordinator
* Natural-language social logistics: *"Let's do a coffee table in Indiranagar tomorrow at 4 PM"*.
* The HiveMind checks availability, generates an interactive RSVP card, and coordinates small-group gatherings effortlessly.

### 7. 🔓 Zero-Cost Free Models via OpenCode
* Pluggable LLM backends: Run 100% free with **OpenCode free models**, self-hosted **Ollama** (Llama 3.3, Mistral), or commercial APIs (Gemini 2.0/3.0, Claude 3.5, GPT-4o).

---

## 🏗️ Architecture & Tech Stack

* **Frontend**: Next.js 15 (App Router), React 19, TypeScript, Tailwind CSS, shadcn/ui.
* **Visual Graph**: `@xyflow/react` (React Flow) / Force-directed graph.
* **Database & Memory**: PostgreSQL 16 with `pgvector` for semantic search + embedded graph storage for relational GraphRAG.
* **Task Queue**: Redis + BullMQ for asynchronous memory ingestion and entity extraction.
* **AI Runtime**: OpenCode CLI/Server bridge, Ollama, or standard OpenAI-compatible endpoints.

For full architectural details, data schemas, and the 4-milestone roadmap, read the [Product Specification](PRODUCT_SPECIFICATION.md).

---

## 📦 Quickstart (Development)

### Prerequisites
* Node.js 20+
* Docker & Docker Compose
* OpenCode CLI (or Ollama / OpenAI API key)

### Local Setup
```bash
# 1. Clone the repository
git clone https://github.com/yashasreddyk/HiveMind.git
cd HiveMind

# 2. Copy environment file
cp .env.example .env

# 3. Start PostgreSQL and Redis via Docker
docker compose up -d postgres redis

# 4. Install dependencies
npm install

# 5. Run database migrations
npm run db:migrate

# 6. Start the development server
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000) to open HiveMind.

---

## 🗺️ Roadmap

- [x] **Product Specification & Architecture Blueprint** (`v1.0.0-DRAFT`)
- [ ] **Milestone 1**: Core Swarm Chat & Next.js 15 App Router Skeleton
- [ ] **Milestone 2**: Synapse Knowledge Graph & React Flow Visualizer
- [ ] **Milestone 3**: Meetup Coordinator & Keeper Governance Dashboard
- [ ] **Milestone 4**: Cross-Hive Federation & MCP Tool Interoperability

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. Check out our [Contributing Guidelines](CONTRIBUTING.md) to get started.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
