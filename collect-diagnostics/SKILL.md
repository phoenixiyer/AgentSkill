---
name: collect_diagnostics
description: >
  Gathers Gemini CLI configuration, extensions, skills, and environment
  information for troubleshooting purposes.
---

Okay, I will help you collect diagnostic information. Please be aware that
you should review the output file for any sensitive information before sharing it.

Here's the plan:
1.  List installed extensions.
2.  List linked skills.
3.  Read the contents of settings.json.
4.  Read the contents of .env if present.
5.  Read the contents of global and project GEMINI.md files.
6.  List relevant environment variables.
7.  Save all information to a file named diagnostic_info.txt.

Let's start:

instruction:
"Run the command `gemini extensions list` and save the output."

instruction:
"Run the command `gemini skills list` and save the output."

instruction:
"Read the file at ~/.gemini/settings.json and save the content."

instruction:
"Check if ~/.gemini/.env exists. If it does, read and save its content."

instruction:
"Read the file at ~/.gemini/GEMINI.md and save the content. If it doesn't exist, note that."

instruction:
"Please provide the path to your project's root directory if you use a project-specific GEMINI.md file."
// Wait for user input, then read the project GEMINI.md //

instruction:
"Run the command `env | grep -E '^GEMINI_|^GOOGLE_'` and save the output."

instruction:
"Combine all the collected information above, clearly labeling each section,
and write it to a file named `diagnostic_info.txt` in the current directory."

