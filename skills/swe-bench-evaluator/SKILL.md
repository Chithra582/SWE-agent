---
name: swe-bench-evaluator
description: "Runs standardized evaluation harnesses against the SWE-bench test split with Docker isolation."
---

# SWE-bench Evaluator

## Overview
The `swe-bench-evaluator` skill orchestrates automated benchmarking against SWE-bench (Full, Lite, and Verified) test datasets.

## Benchmark Execution
- **Isolated Docker Sandboxes:** Run evaluations inside isolated Docker containers matching each repository's exact runtime dependencies.
- **Fail-to-Pass & Pass-to-Pass Tests:** Verify that candidate patches pass newly added unit tests while maintaining green status on existing regression suites.
- **Trajectory Persistence:** Export structured interaction traces for offline ablation analysis.
