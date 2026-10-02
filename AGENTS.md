# AGENTS.md

MATERIALIZED from `docs/build-kuya-hermes.md` on 2026-10-02. This file is a pointer. Edit the canonical build guide, then update this pointer.

Read `docs/index.md` first. Must-haves are PRD-F1 through PRD-F5 in `docs/prd-kuya-hermes.md`. Do not add a generic SQL tool. Do not write purchase orders or shift covers without the confirm step in the `kuya-hermes-ops` skill.

Stack pin that bites: `mcp>=1.2,<2` in `mcp-server/server.py`. Run tools with `uv run`. Hermes home on Windows is `%LOCALAPPDATA%\hermes`.
