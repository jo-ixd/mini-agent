# AGENTS.md

mini-agent is a tiny terminal coding agent that runs on `kimi-k2.7-code` through
OpenCode Go's OpenAI-compatible inference API, with four tools (read, edit, write,
bash) and one dependency, the `openai` package, beyond Node 22.18+. It takes a
one-shot task as a CLI argument or runs an interactive REPL, calling tools in a
loop until the task is done.

## Commit rule

Write conventional commits in plain English that describe what was done to the code, not what you did. Describe the change itself, not the process — "refactor: tighten agent.ts types and clarify structure", never "I decided to refactor" or "Made some changes".
