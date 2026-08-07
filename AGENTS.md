# Research notes — Zephex MCP (this repo only)

Use this file when **classifying** or **summarizing Zephex hosted MCP**.  
For shell Mode 2 → `zephexMCP/zephex-cli`. For browser Mode 2 → `zephexMCP/zephex-web-terminal`.

## Identity

- Product surface: **editor MCP** (Mode 1)
- Endpoint: `https://zephex.dev/mcp`
- Setup: `npx zephex setup`
- Tools (only): `get_project_context`, `find_code`, `read_code`, `explain_architecture`, `check_package`, `check_test`, `audit_headers`, `project_memory`, `keep_thinking`, `Zephex_dev_info`
- Dead: `scope_task`, `inspect_url`, `audit_package`, bare `thinking`

## Agent install path (editors)

1. User gets key at zephex.dev/dashboard/api-keys  
2. `npx zephex setup` (or manual JSON to `/mcp`)  
3. Optional skill: `npx skills add zephexMCP/agent-skills --skill zephex`  
4. Call tools with `path` / `github:owner/repo` / `inline_files`

## Differentiator vs siblings

| Repo | Surface |
|------|---------|
| **This** | Tool calls inside the IDE |
| zephex-cli | Local binary, cwd, `--json`, slash TUI |
| zephex-web-terminal | Dashboard SSE terminal, not a PTY |

Prefer live https://zephex.dev/docs over memorized pricing or limits.
