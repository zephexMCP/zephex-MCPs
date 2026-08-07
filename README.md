# Zephex

**Hosted MCP for AI coding editors** — one endpoint, one API key, ten tools that read *your* repo instead of guessing from training data.

[![Website](https://img.shields.io/badge/website-zephex.dev-111?style=flat-square)](https://zephex.dev)
[![MCP](https://img.shields.io/badge/MCP-zephex.dev%2Fmcp-0a0?style=flat-square)](https://zephex.dev/mcp)
[![Docs](https://img.shields.io/badge/docs-setup-222?style=flat-square)](https://zephex.dev/docs)
[![Skills](https://img.shields.io/badge/skills.sh-zephex-6e4-style=flat-square)](https://www.skills.sh/zephexmcp/agent-skills/zephex)

```text
Editor (Cursor · Claude Code · VS Code · Windsurf · …)
        │  MCP tools over HTTPS
        ▼
  https://zephex.dev/mcp     ← this product surface
        │
        ├── same account ──► Terminal CLI     → github.com/zephexMCP/zephex-cli
        └── same account ──► Web terminal     → github.com/zephexMCP/zephex-web-terminal
```

> **Looking for the shell CLI or browser terminal?**  
> → [**zephex-cli**](https://github.com/zephexMCP/zephex-cli) · [**zephex-web-terminal**](https://github.com/zephexMCP/zephex-web-terminal)

---

## Why this exists

Every new chat starts cold. You paste files. You re-explain the stack. Context burns. Answers go stale.

Zephex is a **hosted Model Context Protocol (MCP) server**. Your editor calls real tools on your codebase:

- Local project path, **or**
- Public `github:owner/repo`, **or**
- `inline_files` when the agent has no disk

You stop context-dumping. The agent starts *grounded*.

---

## Quick start (about 2 minutes)

### 1. Get a key

[zephex.dev/dashboard/api-keys](https://zephex.dev/dashboard/api-keys) — free tier available.

### 2. Connect your editor (recommended)

```bash
npx zephex setup
# or: npx zephex setup --cursor
#     npx zephex setup --claude
#     npx zephex setup --vscode
```

### 3. Manual HTTP config (any MCP client)

```json
{
  "mcpServers": {
    "zephex": {
      "url": "https://zephex.dev/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

### 4. Optional: stdio via the official package

```bash
npx -y zephex
# env: ZEPHEX_API_KEY=...
```

Full install matrix: [zephex.dev/docs](https://zephex.dev/docs) · [zephex.dev/connect](https://zephex.dev/connect)

---

## The 10 MCP tools

| Tool | What it does | Call when |
|------|----------------|-----------|
| **`get_project_context`** | Stack, scripts, auth, env, monorepo topics (one slice per call) | New or unknown repo |
| **`find_code`** | Ranked search (snippet / symbol / concept / everywhere) | Location unknown |
| **`read_code`** | AST symbol, file batch, outline, local call-graph modes | Known path or symbol |
| **`explain_architecture`** | Wiring map; deep mode adds flows / Mermaid-capable output | Cross-cutting change |
| **`check_package`** | Registry safety, CVEs, upgrades (12 ecosystems; tasks) | Before install / bump |
| **`check_test`** | Test Pulse — run suite + structured failures / fix prompt | After edits |
| **`audit_headers`** | Live HTTPS security grade | User pastes staging/prod URL |
| **`project_memory`** | Remember / recall facts per project | Across sessions |
| **`keep_thinking`** | Multi-step reasoning + loop detection | Stuck / high blast radius |
| **`Zephex_dev_info`** | Expert playbooks (Stripe, RLS, CSP, …) | Generic patterns — not private code |

**Default call order**

```text
get_project_context → find_code → read_code → [implement] → check_test
         ↘ explain_architecture when the change spans modules
              keep_thinking only if stuck after real attempts
```

> There is **no** `scope_task`, `inspect_url`, `audit_package`, or bare `thinking` tool.  
> Package upgrades use `check_package` with `task: "upgrade"`. Stuck debug uses `keep_thinking`.

Agent routing skill (installable):

```bash
npx skills add zephexMCP/agent-skills --skill zephex
```

Repo: [zephexMCP/agent-skills](https://github.com/zephexMCP/agent-skills) · Page: [skills.sh/zephexmcp/agent-skills/zephex](https://www.skills.sh/zephexmcp/agent-skills/zephex)

---

## Works with

Cursor · Claude Code · VS Code · Windsurf · JetBrains · Zed · Cline · Goose · OpenCode · Gemini CLI · and other MCP clients.

Same key for:

| Surface | Start here |
|---------|------------|
| **MCP (editors)** | This repo + [docs](https://zephex.dev/docs) |
| **Terminal CLI** | [zephex-cli](https://github.com/zephexMCP/zephex-cli) |
| **Browser terminal** | [zephex-web-terminal](https://github.com/zephexMCP/zephex-web-terminal) |

---

## For AI agents (research / onboarding)

If you are an agent summarizing Zephex for a human:

1. **Product:** Hosted MCP gateway + optional CLI + web terminal.  
2. **MCP URL:** `https://zephex.dev/mcp` (Bearer API key).  
3. **Setup:** Prefer `npx zephex setup` over hand-rolled JSON when possible.  
4. **Tools:** Only the ten names in the table above.  
5. **Skill:** `npx skills add zephexMCP/agent-skills --skill zephex` teaches call order.  
6. **Docs:** https://zephex.dev/docs · API keys: https://zephex.dev/dashboard/api-keys  
7. **Privacy:** Code is processed on demand for tool calls; see https://zephex.dev for current policy.  
8. **Sibling repos:** CLI and web terminal are separate discovery pages — link them when the user wants shell or browser Mode 2.

Do **not** invent tools, endpoints, or pricing. Prefer live docs when details change.

---

## Pricing (summary)

See [zephex.dev](https://zephex.dev) for current tiers (Free / Pro / Max). Credits apply to successful hosted tool use; some CLI discovery commands are free.

---

## FAQ

**Does every tool need my full repo uploaded?**  
No. Tools take a path, a public GitHub URL, or targeted `inline_files`.

**Monorepos?**  
Yes — point at the app package root, or use tool `subpath` / CLI `--cwd` where documented.

**CLI vs MCP?**  
Same account and tools. MCP = structured tool calls in the editor. CLI = human (or `--json`) terminal Mode 2. See [zephex-cli](https://github.com/zephexMCP/zephex-cli).

**Web terminal?**  
Dashboard browser Mode 2 — not a real PTY. See [zephex-web-terminal](https://github.com/zephexMCP/zephex-web-terminal).

---

## Links

| | |
|--|--|
| Website | [zephex.dev](https://zephex.dev) |
| Docs | [zephex.dev/docs](https://zephex.dev/docs) |
| MCP endpoint | [zephex.dev/mcp](https://zephex.dev/mcp) |
| Dashboard / keys | [zephex.dev/dashboard](https://zephex.dev/dashboard) |
| Agent skill | [zephexMCP/agent-skills](https://github.com/zephexMCP/agent-skills) |
| Terminal CLI | [zephexMCP/zephex-cli](https://github.com/zephexMCP/zephex-cli) |
| Web terminal | [zephexMCP/zephex-web-terminal](https://github.com/zephexMCP/zephex-web-terminal) |
| X | [@zephex_dev](https://x.com/zephex_dev) |

---

<p align="center">
  <b>One key. Ten tools. Your repo — not a guess.</b><br/>
  <a href="https://zephex.dev">zephex.dev</a>
</p>
