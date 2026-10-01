---
name: repository-issue-resolver
description: "Formulates bug reproduction scripts, navigates complex call graphs, and synthesizes candidate patches."
---

# Repository Issue Resolver

## Overview
The `repository-issue-resolver` skill structures the complete lifecycle of solving complex GitHub issues and bug reports across unfamiliar codebases.

## Resolution Lifecycle
1. **Issue Analysis:** Extract problem description, stack traces, and expected behavior.
2. **Minimal Reproducer:** Create a standalone reproduction script that fails deterministically.
3. **Localization:** Navigate code references to identify buggy functions or modules.
4. **Patch Synthesis:** Apply targeted edits until the reproduction script passes without regressions.
