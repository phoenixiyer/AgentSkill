---
name: forensic-audit
description: >
  Performs a deep-state forensic audit to identify token leaks and hidden 
  backend prompt amplification. Generates a comprehensive `gemini_diagnostic_report.md` 
  containing global/local configs, MCP health, and usage stats.
---

I am initiating a deep-state forensic audit of the Gemini CLI environment. My goal is to determine the "Prompt Amplification Factor" and identify why your quota is being exhausted.

instruction:
"Create or overwrite a file named `gemini_diagnostic_report.md` in the current directory. Start it with a header: '# Gemini CLI Forensic Diagnostic Report' and the current timestamp."

instruction:
"Run `gemini extensions list`, `gemini skills list`, and `gemini /mcp list`. Append the output of these commands to `gemini_diagnostic_report.md` under a '## System Components' section."

instruction:
"Read the global `~/.gemini/settings.json` and `~/.gemini/GEMINI.md`. Append their contents to the report. Specifically, check if `experimental.enableAgents` is true, as this is the primary driver of hidden prompts."

instruction:
"Check for local project overrides: Read `./.gemini/settings.json`, `./GEMINI.md`, and `./.env` (masking API keys). Append these to the report. If a local `GEMINI.md` exists, calculate its character count and flag it if it exceeds 3,000 characters."

instruction:
"Execute `gemini /stats` to get real-time token consumption. Append this to a '## Usage Statistics' section in the report."

instruction:
"Capture relevant environment variables by running `env | grep -E '^(GEMINI_|GOOGLE_)'`. Append these to the report to check for project/model overrides."

instruction:
"Forensic Log Analysis: Locate the telemetry log path from settings.json (typically `.gemini/telemetry.log`). Use a shell command to count the number of '\"role\": \"user\"' entries in the last 50 lines. If the ratio of internal 'user' roles to your actual requests is > 3:1, explicitly write a warning in the report about 'Hidden Agent Looping'."

instruction:
"Finalize the report by adding a '## Debugging Insights' section. Based on the gathered data, provide a summary of whether the quota issue is caused by: 1. Failing MCP servers causing retries, 2. Instruction bloat (massive GEMINI.md), or 3. Agentic loops (experimental features)."

instruction:
"Output a message to the user confirming that `gemini_diagnostic_report.md` has been generated and is ready for review."
