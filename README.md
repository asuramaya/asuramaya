# asuramaya

I build tools that reduce friction between humans and machines.

Most of the work lives where operators have to deal with complexity directly: workflow systems, MCP servers, inspection tools, audit surfaces, autonomous agents, and infrastructure that makes hidden state easier to see.

## Selected Work

- [`neo`](https://github.com/asuramaya/neo) — local workflow forensics for Claude Code: agent transcripts, reminder injections, telemetry leftovers, and hook-visible lifecycle events surfaced into a single SQLite database with explicit measured / estimated / inferred labels.
- [`chronohorn`](https://github.com/asuramaya/chronohorn) — family-agnostic experiment tracking and architecture search, with a 64-tool MCP surface for driving runs, comparing curves, and ranking frontiers.
- [`heinrich`](https://github.com/asuramaya/heinrich) — model forensics through geometry: residual-stream projections, activation traces, attention routing, and inspection surfaces for what models actually compute.
- [`remix-etherscan-mcp`](https://github.com/asuramaya/remix-etherscan-mcp) — a smart-contract audit MCP that combines Etherscan v2, `remixd`, git context, contract compilation, fork simulation, and post-deploy inspection.
- [`exciton`](https://github.com/asuramaya/exciton) — OSS crypto-influencer engine for Solana: deterministic on-chain scanning plus an LLM-driven trading agent in one Rust workspace. [madapesai.com](https://madapesai.com) is the reference deployment.
- [`ndrchst`](https://github.com/asuramaya/ndrchst) — Python-based Minecraft server management for Paper/Velocity fleets, backups, templates, compatibility layers, and remote orchestration.
- [`decepticons`](https://github.com/asuramaya/decepticons) — reusable predictive primitives for substrates, memory, gating, routing, and readouts. The kernel under `chronohorn`.

## What Ties It Together

- The interface keeps changing; the work underneath doesn't — make systems easier to run, inspect, and trust.
- I optimize for operator clarity over polished abstraction. My better projects keep their state and failure surfaces in plain view, evidence included.
- Most of it is machine-facing. None of it is locked to one model family or one product category. The throughline is practical control over hard systems.

## Lineage

- [`Like-Us`](https://github.com/asuramaya/Like-Us) is the oldest and messiest repo in the set. It still matters as an origin point: the mechanistic branch fed into `decepticons`, `chronohorn`, and `heinrich`, while the safety branch eventually looped back into later jailbreak and forensics work.

## Background

Six years across enterprise IT, public ops, and independent engineering, all out of Houston, TX. Mostly it's been the same work: take ownership of messy systems and cut down the guesswork operators have to do.

Links: [website](https://asuramaya.com/) · [GitHub](https://github.com/asuramaya) · [LinkedIn](https://www.linkedin.com/in/hector-chavez-291765237)
