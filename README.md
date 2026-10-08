# mini-agent

A tiny terminal coding agent using OpenRouter's `z-ai/glm-5.3-flash`.
One TypeScript source file, under 100 lines, no packages, native Node TypeScript,
and raw `fetch`. Requires Node **22.18+** (Node 24 recommended) and Bash.

## Run

```bash
export OPENROUTER_API_KEY='your-key'
node agent.ts
# Or give it one task and exit:
node agent.ts 'Inspect this project, fix the failing test, and verify the fix.'
```

Alternatively, copy `.env.example` to `.env`, fill in your key, and run:

```bash
node --env-file=.env agent.ts
```

No install or build step. `npm start` also works with an exported key.
Type `/exit` to quit; conversation history lives in memory for that session.

To work on another project, change into that project and run this file by its
absolute path. Tools use the terminal's current working directory.

## Four tools

- `read_files`: read an array of UTF-8 file paths.
- `edit_files`: apply exact, unique text replacements to existing files.
- `bash`: run a command with a 60-second timeout; failures return output to the model.
- `write_files`: create or overwrite files, creating parent directories.

The model can call tools repeatedly until it finishes. Calls execute sequentially;
tool errors go back to the model so it can recover. Each user turn is capped at
50 model requests, requests time out after 120 seconds, and tool results are
truncated at 20,000 characters. There is no streaming or persistent history.
Batch file operations are not atomic: earlier entries may succeed before a later
entry fails.

**Only run in a trusted workspace.** There is no sandbox or approval prompt:
the agent can read/write any path your user can access and run arbitrary Bash.
Prompts and tool outputs are sent to OpenRouter and its model provider. Requests
can incur charges. Never commit API keys.

For local mock testing, `OPENROUTER_BASE_URL` can override the API base URL;
normally leave it unset so requests go to `https://openrouter.ai/api/v1`.

## Verification

Verified on Node 24.19.0 using a local mock OpenRouter server: all four tools,
multi-step tool use, tool-error recovery, reasoning-message preservation, output
limits, HTTP/provider errors, missing credentials, and interactive input/exit.
The real model ID was checked against OpenRouter's model catalog. No live model
request was made; an API key is needed to verify provider behavior end to end.
