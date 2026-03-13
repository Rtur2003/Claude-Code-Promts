# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Added
- **Multi-Agent Orchestration prompt** — ORCHESTRATE protocol for coordinating multiple Claude Code sessions, agent specialization, shared state management, conflict resolution, and parallel execution patterns (Hub & Spoke, Pipeline, Swarm, Review Loop topologies)
- **Monorepo & Complex Projects prompt** — SCALE protocol for Turborepo/Nx/pnpm workspaces, hierarchical CLAUDE.md strategies, cross-package dependency management, microservices architecture, and CI/CD optimization for multi-package builds
- **Claude Code Setup Guide** — Complete guide for `.claude/` directory structure, `settings.json` specification, custom slash commands (`.claude/commands/`), CLAUDE.md hierarchy design, prompt placement strategies (single prompt, custom commands, layered, team shared), multi-prompt composition patterns, conflict matrix, real-world setup examples (solo dev, team of 5, enterprise monorepo)

### Enhanced
- **README.md** — Added new prompts to catalog, expanded Common Combinations table with multi-agent and monorepo entries, updated repository structure counts, added Setup Guide to resources
- **QUICK-START.md** — Added multi-agent orchestration and monorepo prompts to architecture section, added setup guide reference
- **USAGE.md** — Added multi-agent and monorepo scenarios to prompt selection table
- **Agent Index** — Updated catalog to 30 prompts, added orchestration and monorepo entries
- **Prompt Index** — Added new prompts and setup guide to catalog

### Changed
- Agent prompt count: 28 → 30
- Workflow guide count: 3 → 4
- Total prompt files: 39 → 41

---

### Added
- **API Design & GraphQL prompt** — SCHEMA protocol for schema-first design, DataLoader, caching, contract testing
- **Cloud & Infrastructure prompt** — CLOUD protocol for IaC, multi-region, K8s, cost optimization
- **Data Engineering prompt** — PIPELINE protocol for dbt, streaming, data quality, Apache Airflow
- **Compliance & Governance prompt** — GOVERN protocol for GDPR, HIPAA, SOC 2, PCI DSS, STRIDE threat modeling
- **Debugging & Troubleshooting prompt** — DEBUG protocol for production debugging, profiling, incident response
- **Blockchain & Web3 project-type prompt** — Solidity, Rust, Foundry, smart contract security, gas optimization
- **Desktop Application project-type prompt** — Tauri, Electron, Qt, native integration, auto-update
- **Cloud Infrastructure example** — Terraform + K8s on AWS real-world deployment walkthrough
- **AI Agent example** — Building an AI-powered code review agent with Claude API
- **Troubleshooting Guide** — Systematic issue diagnosis decision flowchart with common patterns
- Accessibility Audit prompt — ACCESS protocol for WCAG 2.2 compliance testing
- Migration & Upgrade prompt — MIGRATE protocol for framework, database, and dependency migrations
- Monitoring & Observability prompt — OBSERVE protocol for logs, metrics, traces, and alerting
- AI & LLM Integration prompt — AUGMENT protocol for RAG, vector DBs, AI agents, and safety
- Game Development prompt — Unity, Unreal, Godot, ECS, multiplayer patterns
- Embedded Systems & IoT prompt — C, C++, Rust, FreeRTOS, MQTT, TinyML, safety-critical
- Full-Stack App example — Next.js + tRPC + Prisma end-to-end walkthrough
- Security Audit example — Node.js/Express vulnerability assessment walkthrough
- Refactoring example — Legacy code improvement with before/after metrics
- Prompt Selector Guide — Interactive decision tree for choosing the right prompt combination
- CLAUDE.md — AI agent configuration for working on this repository
- LICENSE file (MIT)
- CHANGELOG.md for version tracking

### Enhanced
- **Security Audit prompt** — Added cloud security assessment, supply chain security, zero trust architecture
- **Architecture Patterns prompt** — Added serverless architecture, event sourcing deep dive, saga pattern, data consistency patterns
- **Testing Strategies prompt** — Added contract testing (Pact), property-based testing (Hypothesis, fast-check), chaos testing, anti-patterns table
- **Performance Optimization prompt** — Added GraphQL N+1 prevention, memory profiling (Node.js + Python), CDN/edge optimization, Cloudflare Workers
- **Full-Stack Development prompt** — Added WebSocket/SSE real-time patterns, Socket.io integration, BullMQ background jobs
- **API Development prompt** — Added idempotency keys, cursor-based pagination, webhook delivery with retries
- **Data Science & ML prompt** — Added MLOps section with model monitoring (drift detection), SHAP/LIME explainability, MLflow experiment tracking, model registry
- **Web Development prompt** — Added SEO/meta tags (Open Graph, JSON-LD), font optimization (preload, swap), image optimization (WebP, lazy loading), accessibility quick wins

### Changed
- Updated README.md with all new prompts, expanded combinations table (36 combinations), updated architecture section
- Updated QUICK-START.md with all new prompts and resources
- Updated USAGE.md with new scenarios for all new prompts
- Updated CONTRIBUTING.md with new file counts and contribution types
- Updated all INDEX.md files with new prompt entries and expanded feature matrix
- Made repository fully English-only and global
- Expanded feature matrix to include Blockchain and Desktop columns
- Agent prompt count: 23 → 28
- Project type prompt count: 9 → 11
- Example count: 5 → 7
- Workflow guide count: 2 → 3
- Total prompt files: 32 → 39

### Removed
- Turkish translations directory (repository is now English-only for global accessibility)
- Language support section from README.md
- Language-specific references from all documentation

## [1.0.0] - 2024-01-01

### Added
- Initial release with 19 English agent prompts
- Foundation prompt for interactive sessions
- 7 project-type prompts (Web, API, Data Science, Mobile, DevOps, Database, General)
- APEI methodology (Analyze → Plan → Execute → Iterate)
- Examples: REST API and Debugging walkthroughs
- Workflow guide: Iterative Development Guide
- Documentation: README, QUICK-START, USAGE, CONTRIBUTING
