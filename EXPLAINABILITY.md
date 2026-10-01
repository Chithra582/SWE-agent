# EXPLAINABILITY — SWE-agent Autonomous Software Engineering System

> **Admissibility & Transparency Report for OpenGAP / Agent Passport**  
> *Agent Name:* SWE-agent Autonomous Software Engineering System (`swe-agent`)  
> *Specification:* OpenGAP v0.1.0  
> *Domain:* Developer Tools / Autonomous Software Engineering & Benchmark Evaluation  

---

## 1. Overview & Operational Purpose

The **SWE-agent Autonomous Software Engineering System** (`swe-agent`) is an autonomous software engineering agent created by Princeton NLP, engineered to resolve real-world GitHub issues across large, complex software repositories. Central to its architecture is the Agent-Computer Interface (ACI), a custom-designed suite of terminal and editing commands tailored specifically to make repository navigation, code editing, and test execution efficient and error-free for large language models.

By systematically pairing reproduction scripts, sliding-window code viewing, real-time syntax linting, and automated Docker-isolated test verification, SWE-agent achieves industry-recognized performance on the SWE-bench benchmark with complete explainability and reproducibility.

---

## 2. How the Agent Decides (Decision-Making Logic)

SWE-agent Autonomous Software Engineering System operates across a deterministic, multi-stage decision pipeline:

```
[Stage 1: Issue Ingestion & Triage] ──> [Stage 2: Reproduction Script Creation] ──> [Stage 3: ACI Codebase Navigation]
                                                                                                    │
                                                                                                    ▼
[Stage 6: Patch Submission & PR Generation] <── [Stage 5: Test Suite Verification] <── [Stage 4: Surgical ACI Patch Editing]
```

### 2.1 Issue Ingestion & Triage
- **Decision:** Extracts error traces, problem statements, and target repository details from user prompts or GitHub issue tickets.
- **Rules:** If problem description is ambiguous, explore relevant tests to determine the author's original intent before editing.

### 2.2 Reproduction Script Creation
- **Decision:** Drafts a minimal, self-contained Python reproduction script reproducing the exact failure reported in the issue.
- **Rules:** Confirm that the reproduction script fails on the unpatched codebase before writing any fixes.

### 2.3 ACI Codebase Navigation
- **Decision:** Locates relevant functions using search primitives and inspects lines using 50-line sliding window commands.
- **Rules:** Never dump full files into memory. Maintain cursor tracking across multi-file traces to minimize token consumption.

### 2.4 Surgical Patch Synthesis & Verification
- **Decision:** Applies targeted line replacements and runs automated linters to verify syntax before re-running the reproduction script.
- **Rules:** If the reproduction script fails, inspect the stack trace and iterate up to 5 times. Remove scratch files before final diff generation.

---

## 3. Data & Privacy

| Category | Policy / Handling |
|---|---|
| **Input Data** | In-memory evaluation of repository source files, issue descriptions, and terminal outputs. |
| **Output Artifacts** | Clean unified git diff patches, reproduction test scripts, and execution trajectories. |
| **Telemetry & Logging** | Local deterministic console logging and trajectory JSONL files; zero external analytics telemetry. |
| **Third-Party APIs** | Model inference routed solely through operator-configured API gateways (OpenAI, Anthropic, or local LLMs). |

SWE-agent Autonomous Software Engineering System complies with operational security and privacy standards:
- **No Cloud Data Exfiltration:** Operates locally or in isolated Docker containers without sending proprietary code to unapproved servers.
- **Epistemic Isolation:** Container filesystems and trajectory stores are reset between issue instances, preventing cross-issue data leakage.
- **Sanitized Model Payloads:** Repository credentials, API keys, and environment tokens are scrubbed from prompts.
- **Data Minimization:** Only relevant code windows and command responses are injected into active context windows.

---

## 4. Known Limitations & Failure Modes

Reviewers, auditors, and users should note the following operational constraints:

1. **Complex GUI & Web Browser Interactions**
   - *Limitation:* The agent operates primarily through terminal-based ACIs and cannot natively inspect graphical user interfaces without headless browser tools.
   - *Mitigation:* The agent relies on command-line reproduction scripts and headless test suites for all visual components.

2. **Long-Running Build & Test Pipelines**
   - *Limitation:* Repositories with multi-hour compilation cycles or massive test suites can slow down the iterative feedback loop.
   - *Mitigation:* The agent focuses testing strictly on isolated sub-packages and single unit test files during active development.

3. **Multi-Repository Dependency Tracking**
   - *Limitation:* Bugs spanning multiple interdependent external repositories may require coordinated environment setup beyond a single repo tree.
   - *Mitigation:* The multilingual environment setup skill provisions exact locked package versions matching benchmark specifications.

4. **Flaky Test Suite False Positives**
   - *Limitation:* Non-deterministic tests with network or timing dependencies can occasionally fail regardless of patch validity.
   - *Mitigation:* The agent establishes baseline test results prior to editing and re-runs failing tests to distinguish true regressions.

---

## 5. Verification, Safety & Human Oversight

The agent implements comprehensive oversight mechanisms:
- **Real-Time Human Approval Gate:** Mandatory explicit operator confirmation is required prior to applying patches to production branches, pushing commits, or executing destructive shell commands.
- **Emergency Session Interrupt:** Users can immediately cancel running trajectories at any moment via standard `Ctrl+C` interrupt signals.
- **Step Quota Guardrails:** Autonomous solving loops enforce a default ceiling of 30 steps to prevent runaway exploration.
- **Structured Audit Logging:** Every ACI command, file view, line replacement, and test execution is logged into machine-readable trajectory files for post-run inspection.
