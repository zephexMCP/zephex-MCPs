Zephex

A hosted MCP gateway that gives your AI coding editor a real memory of your project.
One endpoint. One API key. Works with Cursor, Claude Code, VS Code, Windsurf, JetBrains, Zed, Cline, Kiro, Goose, and more — without touching a local config ever again.
→ Get your free API key at zephex.dev

The problem it solves
Every time you open a new chat in Cursor or Claude Code, your AI starts from zero. You paste the same files. You re-explain the stack. Twenty minutes go by before you write a single useful line.
Zephex plugs into your editor as an MCP server and gives it 10 tools that actually understand your codebase — which files matter for this task, what utilities already exist, which callers will break, what the architecture looks like. It reads local directories and remote GitHub repos equally well.

You stop context-dumping. Your AI starts actually helping.

Setup (takes 2 minutes)

Cursor · Windsurf · JetBrains · VS Code
Add this to your editor's MCP settings:

json{
  "mcpServers": {
    "zephex": {
      "url": "https://api.zephex.dev/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}

Claude Code · Zed · Goose · Factory AI

json{
  "mcpServers": {
    "zephex": {
      "command": "npx",
      "args": ["-y", "zephex-mcp"],
      "env": {
        "ZEPHEX_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}


Or use the CLI:
bashnpx zephex-mcp init
Cline · Kiro · OpenCode · Gemini CLI
Use the one-click OAuth flow at zephex.dev/connect — no key to copy.


The 10 tools

Every tool works with either a local absolute path or a GitHub, GitLab, or Bitbucket repo. Private repos are supported with a GITHUB_PAT.

scope_task
Start here for any non-trivial coding task.
Describe what you want to build or fix in plain English. It identifies which files matter, which callers might break, what reusable code already exists, and suggests an approach before you even open a file.
Example: “add a timeout option to the isOnline function”
→ returns focus files, affected callers, suggested approach, and risk level
This typically saves 15–20 minutes per session.

get_project_context
Gives you a full project overview in one call.
Detects language, framework, runtime, package manager, scripts, CI/CD setup, entry points, and dependency health.
Works across Node, Python, Go, Rust, Java, Kotlin, Swift, Dart, Ruby, PHP, .NET, and more.
Example: github:vercel/next.js → TypeScript · Next.js · pnpm · GitHub Actions · 3 outdated dependencies

read_code
Read exactly what you need—no extra noise.
Pull a specific function, symbol, or related code without loading entire files. Supports fuzzy matching and batch lookups.
Modes: symbol, file, outline, callers, blast_radius, dead_code

find_code
Search code with real understanding.
Supports boolean queries, regex, and scoped searches (definitions, usages, tests, imports, config).
Useful before adding new code so you don’t duplicate existing logic.
Example: “stripe AND webhook NOT test” → returns relevant definitions

explain_architecture
Quickly understand how a codebase works.
Ask questions like “how does auth work?” or “what’s the billing flow?”
Returns diagrams, flow explanations, anti-patterns, complexity hotspots, and a health score.
Modes: overview, deep, audit

check_package
Verify a package before installing.
Checks if it exists, isn’t deprecated or typosquatted, and has no malicious install scripts.
Supports npm, PyPI, Cargo, Maven, NuGet, RubyGems, Go modules, and more.

audit_package
Get a full upgrade report before changing versions.
Shows breaking changes, CVEs, migration steps, peer dependency issues, and runtime compatibility.
Example: next @ 13.5.4 → 16.2.1
→ 2 breaking changes · CVE-2025-29927 (CVSS 9.1) · 1 peer dependency conflict

audit_headers
Run after deploying to production.
Checks security headers (CSP, HSTS, COOP, COEP, Permissions-Policy), SSL/TLS config, redirects, and cookie settings.
Returns a grade and ready-to-use fixes for Vercel, Cloudflare, Nginx, and Apache.
Helpful for SOC 2, PCI, and HIPAA compliance.

Zephex_dev_info
Searchable dev knowledge base inside your editor.
Covers topics like Stripe webhooks, Supabase RLS, Convex schemas, CSP/CORS, JWT rotation, AWS ECS, Next.js 16, Bun, Expo signing, and more.

thinking
Structured reasoning for complex tasks.
Tracks your hypotheses, confidence, and findings as you debug or plan changes.
Helps you stay focused and avoid going in circles.
Best for tough bugs, auth refactors, billing systems, database migrations, and post-incident analysis.




Agent skills (new)
If you're building AI agents or running Claude Code in agentic mode, check out zephexMCP/agent-skills — a growing set of pre-built skill definitions optimized for use with Zephex tools. Drop them into your agent config and your AI knows the right call order, fallback patterns, and when to reach for thinking vs scope_task.

Pricing
Free MaxPrice$0$19/ moRequests30/hr300/hrPrivate repos
All 10 tools✅✅


FAQ

Does Zephex send my code anywhere?
No. Code is read on-demand per request and never stored. Privacy policy →
What if my editor can't reach a local path?

Every tool accepts an inline_files fallback — pass file contents as a JSON object directly. Useful in remote/cloud editor environments.
Does it work with monorepos?

Yes. Use focus_on: "services/api" in get_project_context to target a subdirectory.
Can I use it with private GitHub repos?

Yes — set GITHUB_PAT in your environment, or wait for per-user GitHub OAuth (coming soon).
What's the difference vs just pasting files into context?

Pasting files burns your context window and goes stale. Zephex reads only what's needed per task, always from the current state of your repo, and fits in a fraction of the tokens.

links:

Website
Documentation
Pricing
Agent Skills repo
X / Twitter @zephex_dev
Issues & feature requests

BEST MCP IN 2026
