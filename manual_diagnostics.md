**Manual Steps for Customer to Collect Gemini CLI Diagnostic Information**

Please perform the following steps in the environment where you are experiencing the Gemini CLI quota issues and share the redacted output through our secure support case.

1.  **Open a Terminal:** Access the command line interface on the machine where Gemini CLI is installed.

2.  **Get Gemini CLI Version:** Run the following command to capture the installed version:
    ```bash
    gemini --version
    ```

3.  **List Installed Extensions:** Run the following command and save the complete output:
    ```bash
    gemini extensions list
    ```

4.  **Capture Gemini CLI Stats:**
    *   Start Gemini CLI: `gemini`
    *   If the quota issue is reproducible, try to perform the actions that trigger it.
    *   Then, within the Gemini CLI interface, run the following command and save the output:
        ```
        /stats
        ```
    *   You can exit Gemini CLI with `/quit`.

5.  **Locate and Copy Configuration Files:**
    *   **`settings.json`:** Find the `settings.json` file. This is usually located in the `.gemini` directory in your home directory. Common paths are:
        *   Linux/macOS: `~/.gemini/settings.json`
        *   Windows: `%USERPROFILE%\.gemini\settings.json`
        Copy the entire contents of this file.
    *   **`.env` File:** Check for an `.env` file within the same `.gemini` directory (e.g., `~/.gemini/.env`). If it exists, copy its contents.

6.  **Locate and Copy `GEMINI.md` Files:** These files provide context to the AI. Please check the following locations and copy the contents of any `GEMINI.md` files found:
    *   User-level: `~/.gemini/GEMINI.md`
    *   Project-level: The root directory of the project/workspace where you typically run `gemini`, and any parent directories up the tree.

7.  **Check Relevant Environment Variables:** Run the following command in your terminal and provide the output. This lists environment variables that might affect Gemini CLI:
    ```bash
    env | grep -E "^GEMINI_|^GOOGLE_|^NODE_"
    ```
8. **OpenTelemetry Log Collection:** Run the following command and save the complete output:
   *   Ask the customer to configure Gemini CLI to log telemetry to a local file. They should add/update their ~/.gemini/settings.json like this:
     
    ```json
    {
  "telemetry": {
    "enabled": true,
    "target": "local",
    "outfile": ".gemini/telemetry.log",
    "logPrompts": true
  }
}
    ```

10.  **CRITICAL STEP: Review and REDACT Sensitive Information:**
    Before sending any of the collected information, you **MUST** carefully review all text and file contents and remove/redact:
    *   Any API keys, passwords, authentication tokens, or other credentials.
    *   Secret keys or private keys.
    *   Internal hostnames, specific IP addresses, or sensitive network details.
    *   Confidential project names, code snippets, or business logic.
    *   Personal identifiable information (PII).
    *   Any other proprietary or sensitive data.
    *   **When in doubt, redact it.**

11.  **Secure Submission:** Paste the redacted information into our secure Google Cloud Support case. Please clearly label each section (e.g., "Output of `gemini extensions list`", "Contents of `settings.json`", etc.).

Providing this information will greatly help us understand your configuration and diagnose the cause of the excessive requests and connection requests leading to quota issues.
