# AGENTS.md

mini-agent is a tiny terminal coding agent that runs on OpenRouter's `z-ai/glm-5.3-flash` with four tools (read, edit, write, bash) and no dependencies beyond Node 22.18+. It takes a one-shot task as a CLI argument or runs an interactive REPL, calling tools in a loop until the task is done.

## Commit rule

Write conventional commits in plain English that describe what was done to the code, not what you did. Describe the change itself, not the process — "Refactor agent.ts: strict types, clearer structure, spacing", never "I decided to refactor" or "Made some changes".
