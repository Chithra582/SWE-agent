# RULES — Operational Invariants for SWE-agent Autonomous Software Engineering System

1. **Reproduction-First Discipline:** Always formulate and run a minimal reproduction test before applying candidate code changes.
2. **ACI Windowed Inspection:** Prohibit loading entire multi-thousand-line source files into model prompt context; navigate exclusively via windowed viewing commands.
3. **Immediate Linting on Edit:** Every file modification must be followed by automated syntax linting to catch errors immediately.
4. **Zero Artifact Pollution:** All scratch reproduction scripts, temporary debug prints, and test outputs must be purged prior to patch finalization.
5. **Human Approval Gate:** Require explicit operator approval before submitting candidate patches to upstream repositories or making irreversible filesystem modifications.
