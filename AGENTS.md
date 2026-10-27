# AGENTS.md — DeepSeek Harness (DSH)

Cordis-based plugin agent harness. Architecture: [docs/architecture.md](docs/architecture.md). Documentation standards: [docs/AGENTS.md](docs/AGENTS.md).

---

## 1. Operational Directives & Token Conservation
- **Surgical Inspection**: Never read whole files over 100 lines. Use `mcp__xerj__xerj_*` or `rg` to find definitions first; read only 50–70 line slices around targets.
- **Minimal Diffs**: Output concise surgical diffs only. Never echo unchanged functions or rewrite full files.
- **Command Output Capping**: Pipe verbose commands (`2>&1 | tail -n 40` or grep for errors). Never run the full test suite repeatedly; test only the affected file.
- **No Chatty Preambles**: Skip conversational filler, summaries, and narrative logs. Move directly to tool calls and execution.

---

## 2. Core Architecture & Cordis Conventions
- **All contributions are Cordis effects**: Use `ctx.effect()` / `ctx.on()`. Registries must return disposers from `register()`.
- **Waterfall listeners MUST call `next()`**: Omitting `next()` prematurely terminates the delegate chain.
- **Plugins, not loop edits**: Extend behavior via documented extension points. Modifying `agent-loop` requires architectural signoff.
- **Model-visible ⟺ Logged**: Every model input must be reconstructable from `SessionEventMap`. Any new visible input requires a session event.
- **ESM Only**: `"type": "module"`. Use package workspace names across packages and `.ts` in local relative imports. Do not introduce CJS-only exports.
- **Branded IDs**: Cross-boundary identifiers use `Branded<B>` from `dsh-brand`, never raw `string`.
- **Pre-stable APIs**: SQLite migrations use monotonic `SCHEMA_VERSION`. Never overwrite or delete committed session generations.

---

## 3. Essential Commands

```sh
pnpm install                     # Node ^22.19 || >=24
pnpm run build                   # tsc emits types, tsdown bundles runtime
pnpm run typecheck && pnpm run lint
pnpm run test                    # Unit tests (run targeted: pnpm vitest run <file>)
pnpm run test:coverage           # CI gate: 100% per-file coverage on packages/*/*/src
pnpm run test:snapshot -t <name> # Snapshot replays
pnpm dsh --profile headless "task" # Headless run (requires DEEPSEEK_API_KEY)
