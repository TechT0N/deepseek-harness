---
name: market-scout
description: Searches trending GitHub repositories across domains (agents, proxy, backend, fintech), analyzes architectural patterns, and records persistent intelligence briefs into Obsidian.
triggers:
  - "scout github"
  - "market research"
  - "check trending repos"
  - "analyze competitor stack"
---

# Market Scout Skill

Use this skill when the user asks to inspect developer ecosystem trends, compare external repositories with our current stack (TechT0N / ShieldNet), or log architectural intelligence.

## Execution Workflow
1. Execute the scout utility:
   `node /home/trevor/workspaces/scout-tool.mjs <domain>`
   Domains: `agents`, `proxy`, `backend`, `fintech` (or pass a direct query string).
2. Inspect the JSON payload and review the created brief at `/home/trevor/workspaces/vault/30-Market-Scout/`.
3. Provide a concise summary highlighting actionable patterns we can implement.
