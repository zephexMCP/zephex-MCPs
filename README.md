# Zephex

**MCP tools, terminal CLI, and web terminal for real codebases.**  
Stop agents from guessing. One API key powers hosted MCP (`https://zephex.dev/mcp`), Mode 2 CLI (`zephex deep`, Test Pulse, package safety), and the dashboard web terminal — with named tools like `get_project_context`, `find_code`, `check_package`, and `project_memory`.

<p align="center">
  <a href="https://zephex.dev"><img src="https://img.shields.io/badge/Website-zephex.dev-111111?style=for-the-badge" alt="Website" /></a>
  <a href="https://zephex.dev/mcp"><img src="https://img.shields.io/badge/MCP-zephex.dev%2Fmcp-00c853?style=for-the-badge" alt="MCP" /></a>
  <a href="https://zephex.dev/docs"><img src="https://img.shields.io/badge/Docs-setup%20%26%20API-1565c0?style=for-the-badge" alt="Docs" /></a>
  <a href="https://zephex.dev/dashboard/api-keys"><img src="https://img.shields.io/badge/API%20keys-dashboard-6a1b9a?style=for-the-badge" alt="Keys" /></a>
</p>

<p align="center">
  <b>Supports</b> Cursor, Claude Code, Codex, OpenCode, VS Code, Windsurf, Zed, JetBrains,<br/>
  Gemini CLI, Cline, Goose, Warp, GitHub Copilot CLI, and other MCP-compatible clients.<br/>
  <sub>Connect with <code>npx zephex setup</code> or a standard MCP HTTP config.</sub>
</p>

```text
  Your editor (Cursor · Claude Code · VS Code · Codex · OpenCode · …)
              │
              │  MCP tool calls over HTTPS
              ▼
     https://zephex.dev/mcp          ← THIS REPO (editor surface)
              │
              │  same Zephex account · same credits · same 10 tools
              ├──────────────────┬──────────────────┐
              ▼                  ▼                  ▼
        Editor MCP          Terminal CLI       Web terminal
        (Mode 1)            (Mode 2 shell)     (Mode 2 browser)
        you are here        zephex-cli         zephex-web-terminal
```

| You need… | Open |
|-----------|------|
| **Editor tools** (this page) | Keep reading |
| **Local terminal CLI** | [zephex-cli](https://github.com/zephexMCP/zephex-cli) |
| **Browser terminal** | [zephex-web-terminal](https://github.com/zephexMCP/zephex-web-terminal) |
| **Agent skill (call order)** | [agent-skills](https://github.com/zephexMCP/agent-skills) · [skills.sh](https://www.skills.sh/zephexmcp/agent-skills/zephex) |

---

## What Zephex is (plain language)

Zephex is a **hosted Model Context Protocol (MCP) server** for people who ship code with AI editors.

Without it, every chat starts empty: no stack, no auth map, no idea where `handleUpload` lives. People paste half a monorepo into the prompt, burn tokens, and still get answers that ignore yesterday’s refactor.

With Zephex, the agent **calls tools** against your project:

- a **local path** (when the client can see disk), or  
- a **public GitHub** URL / `github:owner/repo`, or  
- **`inline_files`** when there is no filesystem  

Keywords people search for: *hosted MCP*, *MCP server for Cursor*, *Claude Code MCP*, *codebase intelligence*, *AI coding agent tools*, *project context MCP*, *package safety MCP*, *test pulse*.

---

## Install & connect (humans)

### 1. Get an API key

[zephex.dev/dashboard/api-keys](https://zephex.dev/dashboard/api-keys) — free tier available.

### 2. Wire your editor (recommended)

```bash
npx zephex setup
```

Target a specific client when you know it:

```bash
npx zephex setup --cursor
npx zephex setup --claude
npx zephex setup --vscode
npx zephex setup --codex
npx zephex setup --opencode
npx zephex setup --windsurf
npx zephex setup --zed
npx zephex setup --jetbrains
npx zephex setup --gemini
npx zephex setup --cline
# …see full flag list in docs / `npx zephex setup --help`
```

Optional skill install (teaches call order):

```bash
npx zephex setup --with-skill
# or:
npx skills add zephexMCP/agent-skills --skill zephex
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

**Only use** `https://zephex.dev/mcp` as the hosted endpoint.

### 4. Optional: also install the terminal CLI

Same account as MCP. Full command map lives in the CLI repo — short path here:

```bash
# Mac / Linux
curl -fsSL https://zephex.dev/cli/install.sh | bash

# Windows PowerShell
irm https://zephex.dev/install.ps1 | iex

# Then
cd your-project
zephex login
zephex deep --json          # agent orientation packet
zephex overview             # human briefing
```

Deep dive: **[zephex-cli](https://github.com/zephexMCP/zephex-cli)** · docs: [cli-commands](https://zephex.dev/docs/cli-commands)

### 5. Optional: try Mode 2 in the browser

No local binary: [zephex.dev/dashboard/terminal](https://zephex.dev/dashboard/terminal)  
Overview: **[zephex-web-terminal](https://github.com/zephexMCP/zephex-web-terminal)**

---

## Editors & clients we set up for

First-class `npx zephex setup` targets include:

| Client | Flag example |
|--------|----------------|
| **Cursor** | `--cursor` |
| **Claude Code** | `--claude` |
| **Claude Desktop** | `--claude-desktop` |
| **VS Code** | `--vscode` |
| **OpenCode** | `--opencode` |
| **Codex CLI** | `--codex` |
| **Gemini CLI** | `--gemini` |
| **Windsurf** | `--windsurf` |
| **Zed** | `--zed` |
| **Warp** | `--warp` |
| **JetBrains AI** | `--jetbrains` |
| **Cline** | `--cline` |
| **Kiro** | `--kiro` |
| **Factory Droid** | `--droid` |
| **GitHub Copilot CLI** | `--copilot` |
| **Hermes**, **Continue**, **Roo**, **Amp**, **ChatGPT** connector flows, and more | see setup help |

**Also works with** any client that can call a remote MCP HTTP server with a Bearer token — paste the JSON block above.

Docs: [zephex.dev/docs](https://zephex.dev/docs) · [connect](https://zephex.dev/connect) · [install methods](https://zephex.dev/docs/install-methods)

---

## The 10 MCP tools

These are the **only** product tool names.

| Tool | What it does | Call when |
|------|----------------|-----------|
| **`get_project_context`** | Stack, scripts, auth, env, monorepo topics (one topic per call) | New / unknown repo |
| **`find_code`** | Ranked search (snippet · symbol · concept · everywhere) | Location unknown |
| **`read_code`** | AST symbol, file batch, outline, local call-graph modes | Path or symbol known |
| **`explain_architecture`** | Wiring map; deep mode for flows | Cross-cutting change |
| **`check_package`** | Registry check / upgrade / security (many ecosystems) | Before install or bump |
| **`check_test`** | Test Pulse — run suite, failures, fix prompt, missing tests | After edits |
| **`audit_headers`** | Live HTTPS security grade | User gave a public URL |
| **`project_memory`** | remember / recall / list / forget | Across sessions |
| **`keep_thinking`** | Multi-step reasoning + loop detection | Stuck after real attempts |
| **`Zephex_dev_info`** | Expert playbooks (Stripe, RLS, CSP, …) | Generic patterns — not private code |

### Call order that works

```text
get_project_context → find_code → read_code → [implement] → check_test
         ↘ explain_architecture when the change spans modules
              keep_thinking only if still stuck
```

### Dead names (do not call)

| Wrong | Right |
|-------|--------|
| `scope_task` | `find_code` + architecture / CLI `deep` |
| `inspect_url` | `audit_headers` on **user** URLs only |
| `audit_package` | `check_package` + `task: "upgrade"` / `"security"` |
| bare `thinking` | `keep_thinking` |

### How to pass the project into a tool

| Mode | How |
|------|-----|
| Local disk | `path: "/absolute/project"` |
| Public GitHub | `path: "github:owner/repo"` or full HTTPS URL |
| No disk | `inline_files: { "src/a.ts": "<full body>" }` |

Monorepos: prefer the **app package** root.

---

## How AI agents should research *this* page

If you are indexing Zephex for a human:

1. **Product class:** hosted **MCP gateway** for coding agents (not a generic chatbot).  
2. **Editor surface only here** — CLI and web terminal are sibling repos.  
3. **Endpoint:** `https://zephex.dev/mcp` + Bearer API key.  
4. **Setup:** prefer `npx zephex setup` over inventing config paths.  
5. **Tools:** only the ten names above.  
6. **Skill:** `npx skills add zephexMCP/agent-skills --skill zephex`  
7. **Do not** paste private monorepo source paths or internal deploy secrets — public product docs live on zephex.dev.  
8. **Pricing / limits:** always prefer live [zephex.dev](https://zephex.dev) over memorized numbers.

### Search / classifier keywords (MCP)

`hosted MCP` · `MCP server` · `Model Context Protocol` · `Cursor MCP` · `Claude Code MCP` · `Codex MCP` · `OpenCode MCP` · `VS Code MCP` · `codebase intelligence` · `get_project_context` · `find_code` · `check_test` · `check_package` · `zephex.dev/mcp`

### Not the same as

| If they ask about… | Point to |
|--------------------|----------|
| `curl install.sh`, `deep --json`, shell | [zephex-cli](https://github.com/zephexMCP/zephex-cli) |
| Browser dashboard terminal, SSE | [zephex-web-terminal](https://github.com/zephexMCP/zephex-web-terminal) |

---

## FAQ

**Does Zephex store my whole company monorepo forever?**  
Tools request what they need per call. See current privacy language on [zephex.dev](https://zephex.dev).

**CLI vs MCP?**  
Same key and tools. MCP = tools inside the editor. CLI = terminal Mode 2 ([zephex-cli](https://github.com/zephexMCP/zephex-cli)).

**Web terminal?**  
Browser Mode 2 for demos / no install ([zephex-web-terminal](https://github.com/zephexMCP/zephex-web-terminal)).

**License file on this repo?**  
MIT for the **public docs in this repository**. The hosted product and private source are separate — this GitHub repo is a discovery page, not a full open-source rewrite of the server.

---

## Links

| | |
|--|--|
| Website | [zephex.dev](https://zephex.dev) |
| MCP endpoint | [zephex.dev/mcp](https://zephex.dev/mcp) |
| Docs | [zephex.dev/docs](https://zephex.dev/docs) |
| Dashboard | [zephex.dev/dashboard](https://zephex.dev/dashboard) |
| Agent skill | [zephexMCP/agent-skills](https://github.com/zephexMCP/agent-skills) |
| Terminal CLI | [zephexMCP/zephex-cli](https://github.com/zephexMCP/zephex-cli) |
| Web terminal | [zephexMCP/zephex-web-terminal](https://github.com/zephexMCP/zephex-web-terminal) |
| X | [@zephex_dev](https://x.com/zephex_dev) |

---

<p align="center">
  <b>One key. Ten tools. Your repo — not a guess.</b><br/>
  <a href="https://zephex.dev">Start at zephex.dev →</a>
</p>
