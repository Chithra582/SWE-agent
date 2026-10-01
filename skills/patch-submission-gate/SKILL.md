---
name: patch-submission-gate
description: "Validates git diff integrity, ensures test cleanliness, and formats pull request submissions."
---

# Patch Submission Gate

## Overview
The `patch-submission-gate` skill acts as the final verification barrier before a patch is marked as complete, submitted to SWE-bench, or packaged as a pull request.

## Verification Checklist
1. **Clean Git Status:** Remove scratch reproduction scripts, temporary logs, and bytecode caches (`__pycache__`).
2. **Minimal Diff Size:** Ensure the patch contains only changes directly relevant to the issue.
3. **Format PR Message:** Generate a structured summary detailing the root cause, fix rationale, and test results.
