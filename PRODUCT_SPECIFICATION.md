# HiveMind — Open-Source Community Swarm Intelligence Platform
## Product Specification & Architecture Blueprint
**Version:** `1.0.0-DRAFT`  
**Author:** Yashas & Antigravity  
**Repository:** `HiveMind`  
**License:** MIT (Open Source)  
**Target Platform:** Modern Web Application (Desktop & Mobile Web)

---

## 1. Executive Summary & Core Thesis

### 1.1 The Problem with Single-Player AI
Current frontier AI assistants (**Google Gemini, Meta Muse, Apple Intelligence, ChatGPT**) are strictly **single-player, solitary bubbles**. Each user operates in complete isolation:
1. **Zero Collective Memory**: If Alice discovers that a nomad cafe in Bengaluru has upgraded to 500 Mbps fiber or that a landlord is running a scam, Bob’s AI knows nothing about it.
2. **Multi-Party Coordination Failure**: A personal AI cannot solve group coordination (e.g., planning a meetup or consensus decision) because it only represents one person. It cannot negotiate a shared consensus among 5 strangers.
3. **Loss of Tribal Knowledge**: Communities, DAOs, co-living collectives, research labs, and subcultures drown in disjointed Slack/Discord chat histories where insights are permanently lost to scrollback.

### 1.2 The HiveMind Solution
**HiveMind** is an open-source web application that allows any community or creator to host, govern, and interact with a **shared AI collective consciousness (a "Hive")**.

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

## 2. Core Primitives & Domain Model

### 2.1 The Hive (Collective Container)
A Hive is an isolated instance of collective intelligence dedicated to a specific group.
* **Metadata**: Name, slug, avatar, manifesto, taglines, and category (e.g., *Digital Nomads, Tech Founders, Queer Safe Spaces, Indie Hackers, Game Devs*).
* **The Constitution**: A set of human-defined guiding principles that govern how the HiveMind behaves, moderates content, and reasons.
* **Access Control**:
  * **Public**: Anyone with the link can view and interact.
  * **Gated (Invite / Passphrase)**: Requires a secret passkey or one-time invite token.
  * **Vetted (Quiz / Application)**: Requires answering community onboarding questions evaluated by the HiveMind or human Keepers.
  * **Domain-Gated**: Requires an email from an allowed domain (e.g. `@university.edu` or `@company.com`).

### 2.2 The Synapse (Living Knowledge Graph)
The Synapse is the collective brain of the Hive. Unlike a flat vector database that just searches text chunks, the Synapse maintains an **attributed, temporal Knowledge Graph**:
* **Entities**: Nodes representing People, Places, Projects, Events, Deals, Tools, and Opinions.
* **Relations**: Semantic edges connecting entities (e.g., `(Maya)-[is_building]->(Fintech App)`, `(Third Wave Cafe)-[verified_wifi]->(200 Mbps)`).
* **Provenance & Attribution**: Every memory node records:
  * `contributor_id`: Who stated or validated this information.
  * `timestamp`: When it was contributed or last re-verified.
  * `confidence_score`: How many members have agreed or corroborated this fact.
  * `status`: `provisional` (1 mention) $\to$ `corroborated` (multiple members) $\to$ `canon` (verified by Keepers).

### 2.3 Dual Thought Modes (Privacy Architecture)
Members can communicate with the HiveMind in two distinct modes:
1. **Whisper Mode (Private 1-on-1)**:
   * The user talks to the HiveMind in complete privacy.
   * Useful for asking sensitive questions (*"Who in this group is hiring for a frontend dev?"* or *"What was the feedback on my proposal?"*).
   * **The conversation is strictly NOT ingested into the communal knowledge graph.**
2. **Synapse Mode (Public / Collective)**:
   * Insights, recommendations, and discussions are analyzed by the HiveMind's memory synthesis worker.
   * Automatically updates the community knowledge graph and memory for all members.

### 2.4 The Keeper (Governance & Pruning)
To prevent the classic "Microsoft Tay" poisoning attack (trolls feeding garbage data into the AI):
* The creator and appointed moderators have **Keeper privileges**.
* **Memory Dashboard**: Keepers have a visual dashboard to inspect newly formed knowledge graph nodes, edit relations, flag false claims, or prune poisoned memories with 1 click.
* **Consensus Thresholds**: Factual claims about people or places remain "Provisional" until corroborated by multiple trusted members.

---

## 3. Product Features & User Experience

### 3.1 The Collective Canvas (Web Interface)
* **Real-time Live Chat**: Streaming markdown, code blocks, voice transcription, and interactive widget cards.
* **Visual Mind Map (Graph Visualizer)**: An interactive 2D/3D force-directed graph (powered by Three.js / React Flow) allowing members to visually explore what the HiveMind currently knows.
* **Activity & Gathering Coordinator**:
  * Members can say: *"Let's get a coffee table together in Indiranagar tomorrow afternoon."*
  * The HiveMind checks who is nearby and free, crafts an interactive **Meetup Card** with RSVP limits, and coordinates the gathering in real time.
* **Member Directory & Skill Matrix**:
  * The HiveMind automatically maintains an up-to-date map of member expertise, current projects, and open asks without anyone having to fill out tedious profile forms.

---

## 4. Technical Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                            FRONTEND (WEB APP)                               │
│  • Next.js 15 (App Router, React 19)       • Tailwind CSS & shadcn/ui        │
│  • Zustand / TanStack Query                • React Flow (Graph Visualizer)  │
│  • WebSockets / SSE Streaming              • Lucide Icons & Framer Motion   │
└──────────────────────────────────────┬──────────────────────────────────────┘
                                       │ HTTPS / WSS
                                       ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           BACKEND & API LAYER                               │
│  • Next.js Server Actions & API Routes     • Auth: NextAuth.js / Supabase   │
│  • Realtime WebSocket Server (Socket.io)   • Background Workers (BullMQ)    │
└──────────────────┬───────────────────────────────────┬──────────────────────┘
                   │                                   │
                   ▼                                   ▼
┌──────────────────────────────────────┐  ┌───────────────────────────────────┐
│           DATA & MEMORY              │  │           MODEL ENGINE            │
│  • PostgreSQL + pgvector (Embeddings)│  │  • OpenCode Server (Free Models)  │
│  • Graph Engine (SQLite-Graph / Kuzu)│  │  • Ollama (Local Self-Hosted)     │
│  • Redis (Task Queue & Cache)        │  │  • OpenAI / Gemini / Claude APIs  │
└──────────────────────────────────────┘  └───────────────────────────────────┘
```

### 4.1 Technology Stack
* **Frontend Framework**: Next.js 15 (App Router), React 19, TypeScript.
* **Styling & Components**: Tailwind CSS, shadcn/ui, Radix UI primitives.
* **Interactive Graph Visualization**: `@xyflow/react` (React Flow) or `force-graph` for the visual synapse mind map.
* **Database**: PostgreSQL with `pgvector` extension for semantic vector embeddings.
* **Graph Storage**: Embedded graph database (`kuzu` or SQLite-based adjacency graph) for relational GraphRAG.
* **LLM Engine**:
  * **Primary Free Tier**: OpenCode CLI/Server (`opencode run`) providing free model inference.
  * **Self-Hosted Local**: Ollama (Llama 3.3, Mistral, Qwen).
  * **Commercial Backends**: Gemini 2.0 / 3.0 Flash, Claude 3.5 Sonnet, GPT-4o via OpenAI-compatible endpoints.

### 4.2 Autonomous Memory Pipeline (How Memory Forms)
1. **Message Ingestion**: User sends a message in Synapse Mode.
2. **Entity & Relation Extraction**: A lightweight extractor prompt identifies entities, claims, sentiment, and confidence.
3. **Graph Reconciliation**:
   * If the entity exists, updates the edge or creates a temporal version.
   * If new, generates an embedding and inserts the node into the Knowledge Graph.
4. **GraphRAG Retrieval**:
   * When another member asks a question, the system performs a hybrid search: Vector Similarity (pgvector) + 2-hop Graph Traversal (Entities/Relations).
   * Context is assembled with strict contributor citations: *"According to @arjun (2 hours ago)..."*.

---

## 5. Security, Trust & Anti-Poisoning Framework

1. **Strict Provenance**: Every piece of knowledge is permanently tagged with the author's user ID and timestamp. Anonymous malicious poisoning is impossible.
2. **Keeper Veto & Undo**: A 1-tap "Purge Memory" button allows community admins to roll back any memory node created by a specific user or within a specific time window.
3. **Prompt Injection Boundary**: All ingested memory nodes are sanitized and wrapped in strict `<community_context>` delimiters with system prompts instructing the model to treat stored knowledge as historical human statements, never as system instructions.
4. **Whisper Isolation Guarantee**: Database-level isolation prevents any Whisper Mode message from ever hitting the embedding generation queue or vector store.

---

## 6. Open Source Deployment & Self-Hosting

HiveMind is built to be **100% self-hostable in under 5 minutes** via Docker Compose:

```bash
git clone https://github.com/yashasreddyk/HiveMind.git
cd HiveMind
cp .env.example .env
docker compose up -d
```

### Included Services in Docker Compose:
* `web`: Next.js 15 application server.
* `postgres`: PostgreSQL 16 with `pgvector`.
* `redis`: Task queue for asynchronous memory ingestion and graph extraction.
* `opencode`: Local OpenCode bridge container for free model access.

---

## 7. Roadmap & Milestone Plan

### Milestone 1: The Core Swarm (Weeks 1–2)
* [ ] Next.js 15 project initialization with TypeScript, Tailwind CSS, and shadcn/ui.
* [ ] Database schema setup (Users, Hives, Memberships, Messages, KnowledgeNodes, KnowledgeEdges).
* [ ] Multi-turn chat interface with streaming responses.
* [ ] OpenCode free models integration via local API bridge.
* [ ] Basic Whisper Mode vs. Synapse Mode toggle.

### Milestone 2: The Synapse Knowledge Graph (Weeks 3–4)
* [ ] Real-time entity & relation extraction worker.
* [ ] Hybrid GraphRAG retriever (pgvector + relational graph traversal).
* [ ] Interactive React Flow Knowledge Graph visualizer.
* [ ] Keeper Memory Management dashboard (edit, approve, prune).

### Milestone 3: Collective Coordination & Meetups (Weeks 5–6)
* [ ] Autonomous Meetup & Gathering Coordinator card generation.
* [ ] Public shareable RSVP links for non-members.
* [ ] Multi-Hive hosting (one instance hosting multiple distinct communities).
* [ ] Invite gating, vetting quizzes, and domain whitelisting.

### Milestone 4: Federation & Extensibility (Future)
* [ ] Cross-Hive federation (two allied Hives can selectively bridge knowledge).
* [ ] MCP (Model Context Protocol) tool integration for external actions.
