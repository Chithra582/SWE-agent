---
name: aci-code-editor
description: "Agent-Computer Interface (ACI) for windowed file viewing, surgical replacement, and syntax linting."
---

# ACI Code Editor

## Overview
The `aci-code-editor` skill leverages Princeton's Agent-Computer Interface (ACI) designed specifically for LLMs. Instead of reading entire files, the agent views code through sliding windows, executes search commands, and performs surgical replacements with built-in linting.

## ACI Primitives
- **Windowed Viewing:** Open files using `open <file> <line>` and scroll using `scroll_up` / `scroll_down`.
- **Surgical Edit:** Replace target lines with `edit <start_line>:<end_line>` followed by replacement code.
- **Immediate Linting:** The ACI automatically runs language-specific linters after every edit to catch syntax errors before execution.
