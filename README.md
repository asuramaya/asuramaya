# asuramaya

I build tools that reduce friction between humans and machines.

Most of the work lives where operators have to deal with complexity directly: workflow systems, MCP servers, inspection tools, audit surfaces, autonomous agents, and infrastructure that makes hidden state easier to see.

## Selected Work

- [`neo`](https://github.com/asuramaya/neo) — local workflow forensics for Claude Code: agent transcripts, reminder injections, telemetry leftovers, and hook-visible lifecycle events surfaced into a single SQLite database with explicit measured / estimated / inferred labels.
- [`chronohorn`](https://github.com/asuramaya/chronohorn) — family-agnostic experiment tracking and architecture search, with a 64-tool MCP surface for driving runs, comparing curves, and ranking frontiers.
- [`heinrich`](https://github.com/asuramaya/heinrich) — model forensics through geometry: residual-stream projections, activation traces, attention routing, and inspection surfaces for what models actually compute.
- [`remix-etherscan-mcp`](https://github.com/asuramaya/remix-etherscan-mcp) — a smart-contract audit MCP that combines Etherscan v2, `remixd`, git context, contract compilation, fork simulation, and post-deploy inspection.
- [`exciton`](https://github.com/asuramaya/exciton) — OSS crypto-influencer engine for Solana: deterministic on-chain scanning plus an LLM-driven trading agent in one Rust workspace. [madapesai.com](https://madapesai.com) is the reference deployment.
- [`ndrchst`](https://github.com/asuramaya/ndrchst) — Rust-based Minecraft server management for Paper/Velocity fleets, backups, templates, compatibility layers, and remote orchestration.
- [`decepticons`](https://github.com/asuramaya/decepticons) — reusable predictive primitives for memory, routing, substrates, and readouts. The kernel under `chronohorn`.

## What Ties It Together

- The interface changes, but the job stays the same: make systems easier to run, inspect, and trust.
- I care more about operator clarity than polished abstraction. The better projects keep state, evidence, and failure surfaces visible.
- A lot of the work is machine-facing, but not narrowly about one model family or one product category. The point is practical control over difficult systems.

## Lineage

- [`Like-Us`](https://github.com/asuramaya/Like-Us) is the oldest and messiest repo in the set. It still matters as an origin point: the mechanistic branch fed into `decepticons`, `chronohorn`, and `heinrich`, while the safety branch eventually looped back into later jailbreak and forensics work.

## Background

Six years across enterprise IT, public ops, and independent engineering in Houston, TX. The work has mostly been about owning messy systems, improving visibility, and reducing operator guesswork.

Links: [website](https://asuramaya.com/) · [GitHub](https://github.com/asuramaya) · [LinkedIn](https://www.linkedin.com/in/hector-chavez-291765237)
