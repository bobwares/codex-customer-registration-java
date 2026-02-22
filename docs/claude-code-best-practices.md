# Claude Code Best Practices (Synthesized from 28 Community + Official Repositories)

## Purpose
This article distills recurring implementation patterns from official Claude Code repos, high-signal config templates, ecosystem awesome lists, and production-oriented starter kits.

---

## 1) Start with an **official baseline**, then layer opinionated config
**Why:** Teams that begin from official sources avoid brittle setups and can adopt ecosystem additions incrementally.

**Practice**
- Begin with official docs and references (`anthropics/claude-code`, `anthropics/skills`, `anthropics/claude-code-action`).
- Add curated defaults from hardened configs (e.g., Trail of Bits style security defaults) only after your base workflow is stable.
- Keep your customizations in version control (`CLAUDE.md`, settings, hooks, skills).

---

## 2) Treat Claude Code setup as **infrastructure-as-code**
**Why:** Repeatable, reviewable AI behavior is easier to scale than ad hoc personal tweaks.

**Practice**
- Store all config artifacts in repo: settings, hooks, slash commands, sub-agents, MCP config, policy files.
- Add install/sync scripts for workstation bootstrap and backup.
- Use configuration composition/merge tools when supporting many frameworks/teams.

---

## 3) Use a **layered memory model**
**Why:** High-performing setups separate durable conventions from task-level context.

**Practice**
- Keep durable team guidance in `CLAUDE.md` (coding standards, architecture constraints, review rules).
- Store project context docs for domain knowledge and terminology.
- Capture session/turn artifacts (logs, decisions, outcomes) for continuity and auditability.
- Periodically prune memory to reduce prompt bloat and stale instructions.

---

## 4) Build with **specialization**: skills + sub-agents + commands
**Why:** Reusable, narrow capabilities outperform one giant generic prompt.

**Practice**
- Package repeatable expertise as skills (testing, GraphQL, security audit, accessibility, docs).
- Use sub-agents for orchestration patterns (planner/executor/checker).
- Define slash commands for common workflows (triage, fix, review, release prep).
- Add quality gates so specialized agents can verify each other.

---

## 5) Enforce quality through **hooks and verification loops**
**Why:** Automation at lifecycle boundaries prevents drift and catches regressions early.

**Practice**
- Use hooks for pre/post edit checks, formatting, linting, test triggers, and policy checks.
- Adopt “plan → implement → verify → summarize” loops.
- Require objective evidence in outputs (test logs, changed files, rationale).
- Fail fast with clear remediation steps when checks do not pass.

---

## 6) Integrate MCP intentionally (start small)
**Why:** MCP is powerful but quickly becomes noisy without governance.

**Practice**
- Begin with 1–3 high-value MCP servers (issue tracker, docs/context, code intelligence).
- Define role-based access and expected usage per server.
- Document allowed actions and guardrails for write-capable integrations.
- Review MCP usage telemetry and remove low-signal integrations.

---

## 7) Optimize for **token economics** and context hygiene
**Why:** Long sessions degrade quality/cost without explicit context management.

**Practice**
- Keep prompts modular and concise; reference docs instead of pasting large blocks.
- Use targeted retrieval (file/path-scoped context) over broad dumps.
- Establish summarization checkpoints for long tasks.
- Track token usage with statusline/monitoring tools.

---

## 8) Adopt **spec-driven execution** for larger initiatives
**Why:** Teams shipping complex features consistently map specs to executable work items.

**Practice**
- Convert PRDs into epics/stories/tasks with explicit acceptance criteria.
- Use parallelization (e.g., worktrees/agent branches) only when task boundaries are clear.
- Preserve traceability from requirement → implementation → verification.

---

## 9) Shift security left with **safe defaults**
**Why:** Agentic coding can magnify both speed and risk.

**Practice**
- Prefer least-privilege permissions and explicit approval boundaries.
- Add secret scanning, dependency checks, and command safelists.
- Include threat-model prompts/checklists for risky changes.
- Keep audit trails of automated actions and external tool invocations.

---

## 10) Bring Claude Code into CI/CD with clear policy boundaries
**Why:** PR/issue automation increases leverage when guardrails are explicit.

**Practice**
- Use `claude-code-action` for scoped PR assistance (Q&A, reviews, targeted code edits).
- Define when AI can comment only vs. propose changes vs. merge-blocking checks.
- Require deterministic checks (tests/lints/security) independent of model output.

---

## 11) Standardize team onboarding and operating model
**Why:** Most failures are process inconsistency, not model capability.

**Practice**
- Provide a starter kit with one-command install and examples.
- Maintain “golden path” docs for daily workflows and incident handling.
- Version your operating playbook and review monthly.

---

## 12) Measure what matters
**Why:** Mature setups track outcomes, not novelty.

**Useful metrics**
- Lead time to merged PR
- Defect escape rate
- Rework rate after AI-generated changes
- Token cost per merged change
- Hook failure categories
- MCP usage quality (signal vs noise)

---

## Reference architecture (practical default)
1. **Core:** official Claude Code + official Skills reference.
2. **Team layer:** shared `CLAUDE.md`, hooks, slash commands, 5–15 core skills.
3. **Execution:** planner/executor/checker sub-agent pattern.
4. **Integrations:** 2–4 MCP servers with explicit access policy.
5. **Automation:** PR workflow via GitHub Action with mandatory CI checks.
6. **Observability:** token/statusline + session log viewer + monthly config review.

---

## Common anti-patterns to avoid
- Installing dozens of skills/plugins before defining your team workflow.
- Using global memory files as unstructured dumps.
- Letting AI-generated output bypass deterministic checks.
- Running too many MCP servers without clear ownership/policy.
- Measuring success by “number of automations” rather than delivery quality.

---

## 30-60-90 day rollout plan
**Day 0–30**
- Deploy baseline config, hooks, and 3 critical commands.
- Pilot with one team and one repo.

**Day 31–60**
- Add specialization: 5–10 skills + planner/checker flow.
- Introduce 1–2 MCP integrations and token monitoring.

**Day 61–90**
- Roll out CI action policy.
- Track delivery + quality metrics; prune low-value configs.
- Publish internal playbook and maintenance cadence.

---

## Bottom line
The strongest Claude Code implementations are **disciplined systems**, not prompt hacks: official baseline, codified team memory, specialized reusable capabilities, strict verification hooks, scoped integrations, and measurable outcomes.
