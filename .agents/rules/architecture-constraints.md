# HiveMind — Architecture Constraints & Guidelines

## 1. Core Product Identity & Mission

> **HiveMind** is an open-source, user-hosted community swarm intelligence platform. It enables groups (digital nomads, subcultures, co-living spaces, startup cohorts, research DAOs) to host, govern, and interact with a shared AI collective consciousness (a "Hive") with an evolving, attributed knowledge graph.

---

## 2. Platform Constraints (Strict Web-Only)

1. **Target Platform**:
   * HiveMind is **strictly a modern Web Application** (Desktop & Mobile Web responsive).
   * **STRICT PROHIBITION**: Do NOT build Android/iOS native mobile wrappers, Android Accessibility Service automation (RPA), PRoot Alpine Linux bridges, or platform-specific OS automation.
   * Rationale: Mobile accessibility automation violates app store policies (Google Play Developer Program Policies ban accessibility abuse for non-disability purposes; Apple iOS strictly forbids background screen reading). A web application provides universal access, 100% platform independence, and effortless self-hosting.
2. **Frontend Architecture**:
   * **Framework**: Next.js 15 (App Router), React 19, TypeScript.
   * **Styling**: Tailwind CSS with `shadcn/ui` components and Radix UI primitives.
   * **Visual Mind Map**: `@xyflow/react` (React Flow) or 2D/3D force-directed canvas.
   * **State & Data Fetching**: TanStack Query (React Query) + Zustand.
3. **Backend & Persistence**:
   * **Database**: PostgreSQL 16 with `pgvector` extension for semantic vector embeddings.
   * **Graph Storage**: Embedded graph store (e.g. SQLite-Graph / Kùzu / relational graph schema) for relational entity-edge traversals.
   * **Asynchronous Queue**: Redis + BullMQ for background entity extraction and graph synthesis.

---

## 3. Pluggable Model Engine & OpenCode Integration

1. **Primary Free Tier (OpenCode)**:
   * HiveMind is designed to run 100% free of cloud API costs using the **OpenCode free model bridge**.
   * Communicates with local OpenCode server/CLI or an OpenAI-compatible bridge.
2. **Self-Hosted Local**:
   * Seamless integration with **Ollama** (Llama 3.3, Mistral, Qwen).
3. **Commercial Fallback**:
   * Direct API adapters for Google Gemini 2.0/3.0, Anthropic Claude 3.5 Sonnet, and OpenAI GPT-4o via user-provided keys.

---

## 4. Dual Thought Modes (Privacy Boundary)

* **Whisper Mode (Private 1-on-1)**:
  * User queries and responses are strictly ephemeral.
  * **Zero Ingestion Guarantee**: Whisper Mode messages MUST NEVER be sent to the entity extraction queue, embedding generator, or vector database.
* **Synapse Mode (Public / Collective)**:
  * Communal discussions and insights are passed to the memory synthesis worker to update the Hive's living Knowledge Graph.

---

## 5. Security & Anti-Poisoning Architecture

1. **Strict Contributor Attribution**:
   * Every memory node in the Knowledge Graph records `contributor_id`, `created_at`, `confidence_score`, and `status`.
   * Anonymous or spoofed memory updates are strictly forbidden.
2. **Keeper Veto & Purge**:
   * Community Keepers (admins) have real-time visibility into new memory nodes and can purge or edit corrupted/troll memories with 1 click.
3. **Prompt Injection Firewall**:
   * Stored community knowledge retrieved during GraphRAG MUST be wrapped inside `<community_context>` delimiters with strict system prompt boundaries instructing the LLM to treat community knowledge as historical member claims, never as executable system instructions.
