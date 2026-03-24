# Gemini CLI Agent Diagnostic Toolkit

### *Troubleshooting Quota Exhaustion, Configuration Overheads, and Agentic Loops.*

This repository contains specialized **Gemini CLI Skills** designed to help developers and SREs identify the "Smoking Gun" behind unexpected token consumption. 

In many cases, quota exhaustion is not caused by the user's primary prompt, but by the **Prompt Amplification Factor (PAF)** where internal agent reasoning, failing MCP servers, or massive instruction bloat trigger multiple hidden backend requests.

---

## Included Skills

### 1. `sys-audit`
A lightweight diagnostic tool to verify the environment state.
*   **Tier Verification:** Detects if the user is on the "Individual" (Free) vs. "Enterprise/Standard" tier.
*   **Config Mapping:** Identifies Global (`~/.gemini/`) vs. Local project-level configurations.
*   **Extension Audit:** Lists active extensions and skills currently loaded into the session.

### 2. `forensic-audit`
A deep-state diagnostic tool designed to bypass "Blocked Call" loops and tool-hallucinations.
*   **Telemetry Analysis:** Analyzes the `telemetry.log` to calculate the ratio of backend agent prompts to user inputs.
*   **MCP Health Check:** Directly pings MCP servers (e.g., `gitlab`, `google-maps`) to identify retry-loops caused by connection failures.
*   **Auto-Redaction:** Uses `sed` logic to mask `AIza...` API keys and sensitive environment variables in the generated report.

### 3. `Manual-Steps`
If the CLI is hanging or you want to avoid further API costs, follow the steps in manual diagnostic guide.

---

## Getting Started

### Installation
1.  Ensure you are on the latest version of the Gemini CLI:
    ```bash
    brew upgrade gemini-cli
    ```
2.  Clone this repository and copy the desired `.md` files to your local skills directory:
    ```bash
    cp ./skills/*.md ~/.gemini/skills/
    ```

### Usage
To generate a comprehensive diagnostic report (`report.md`) in your current directory, run:
```bash
gemini --skill forensic-audit
```
OR
in Gemini CLI Terminal
```bash
Help me collect the forensic audit or collect diagnostic
```

---

## Safe Harbor & Disclaimer

> [!IMPORTANT]
> **Experimental Status:** The skills and scripts provided in this repository are **experimental** and are intended for diagnostic and troubleshooting purposes on nonprod/testing environments only.
>
> **Not an Official Product:** This is **not** an official Google product. These tools are provided "as-is" without any express or implied warranties. Use of these scripts is at the user’s own risk. 
>
> **Data Privacy & Redaction:** While the `forensic-audit` skill includes basic regex-based redaction for API keys, it is the **user's sole responsibility** to review any generated reports for sensitive, proprietary, or confidential information before sharing them with external parties or support teams.
>
> **Support:** These tools are maintained on a best-effort basis. Issues should be tracked via the GitHub repository, but they do not come with a Service Level Agreement (SLA) or official support from Google Cloud.

---

## Troubleshooting Insights
If the `forensic-audit` skill hangs, it is likely because your `LocalAgentExecutor` is blocking the shell tools. To bypass this, manually run the shell commands found inside the `SKILL.md` directly in your terminal. This will generate the same report with **zero** API cost and no risk of "Agent Loops."
