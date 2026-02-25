<div align="center">

# Doctor

**42 automated checks across 6 layers. Security first.**

*A Claude Code skill that scans any project and diagnoses automation gaps — missing security checks, broken hooks, absent tests, misconfigured CI. Then prescribes and applies project-specific fixes.*

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-7C3AED?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iMTAiIGZpbGw9IndoaXRlIi8+PC9zdmc+)](https://docs.anthropic.com/en/docs/claude-code/)
[![Checks](https://img.shields.io/badge/Checks-42-blue?style=for-the-badge)](https://github.com/SomeStay07/claude-doctor-skill#6-layers-42-checks)
[![Layers](https://img.shields.io/badge/Layers-6-orange?style=for-the-badge)](https://github.com/SomeStay07/claude-doctor-skill#6-layers-42-checks)
[![Stacks](https://img.shields.io/badge/Stacks-20+-teal?style=for-the-badge)](https://github.com/SomeStay07/claude-doctor-skill#multi-stack-support)
[![License: MIT](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)](LICENSE)
[![Telegram](https://img.shields.io/badge/Telegram-Channel-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/codeonvibes)

[What It Does](#what-it-does) · [6 Layers](#6-layers-42-checks) · [Install](#installation) · [Usage](#usage) · [How It Works](#how-it-works) · [Example Output](#example-output) · [Multi-Stack](#multi-stack-support)

```bash
curl -sSL https://raw.githubusercontent.com/SomeStay07/claude-doctor-skill/main/install.sh | bash
```

---

</div>

## The Problem

You set up Claude Code in a new project and start coding. Everything seems fine — until you realize:

- Secrets are committed to git history
- `.env` files are world-readable (permissions `644`)
- No pre-commit hooks catch broken code before push
- No CI runs tests automatically
- Claude has no memory of past decisions across sessions
- No domain rules — Claude makes the same mistakes over and over

You don't know what you don't know. And fixing these gaps manually takes hours of research.

## What It Does

**Doctor** is a set of `.md` files that turns [Claude Code](https://docs.anthropic.com/en/docs/claude-code/) into a project automation auditor. Run `/doctor` and get a full health report with severity levels, explanations, and one-click fixes.

> **What's a Claude Code skill?** A skill is a `.md` file in `.claude/skills/` that gives Claude Code specialized behavior for a specific task. No plugins, no API keys — just text files with instructions. [Learn more](https://docs.anthropic.com/en/docs/claude-code/)

Every finding is **project-specific** (not a generic template) and explains **WHY** it matters, with a source link.

### `/doctor scan` — Diagnose

<div align="center">
<br>
<img src="assets/demo-scan.gif" alt="doctor scan demo — diagnosing project health" width="800">
<br>
<sub>Phase 1-2: Study your project, run 42 checks, score each layer</sub>
<br><br>
</div>

### `/doctor fix` — Prescribe + Apply

<div align="center">
<br>
<img src="assets/demo-fix.gif" alt="doctor fix demo — applying fixes" width="800">
<br>
<sub>Phase 3-4: Severity-tagged findings with one-click fixes, then verification</sub>
<br><br>
</div>

## At a Glance

- 42 checks across 6 security & automation layers
- Auto-discovers your stack (20+ languages/frameworks) before any checks
- Every finding has severity + WHY + source link — no vague advice
- Applies project-specific fixes (not generic templates)
- Built-in false positive filtering (14 rules — won't nag about irrelevant things)
- Self-validates findings before output (no inflated severity, no duplicates)
- Incident response playbook for secret leaks (9-step recovery plan)
- Graceful degradation — handles missing git, no tests, context overflow
- Zero dependencies, zero config — just `.md` files
- Bilingual: English and Russian (auto-detects your language)

| Feature | Doctor | [memory-skill](https://github.com/SomeStay07/claude-memory-skill) | [code-reviewer](https://github.com/SomeStay07/code-review-agent) |
|:--------|:------:|:------------:|:---------------:|
| Total checks | **42** | N/A | N/A |
| Layers | **6** | 1 | 1 |
| Auto-discovery (DCI) | **Yes** | Yes | No |
| Error recovery | **Yes** | No | Yes |
| Self-check before output | **Yes** | No | Yes |
| False positive filtering | **14 rules** | No | Yes |
| Incident response | **9-step plan** | No | No |
| Multi-stack | **20+** | No | TypeScript/React |
| Security audit | **11 checks** | No | Partial |
| Scoring & grading | **Yes** | No | No |
| One-line install | **Yes** | Yes | Yes |

## 6 Layers, 42 Checks

Layers are ordered by priority — you can't work on DX if Security is broken:

| Layer | Name | Checks | What It Covers |
|:------|:-----|:------:|:---------------|
| 0 | **Security** | 11 | Secrets in git, SAST, .gitignore, .env permissions, Docker security, client-side keys, incident response |
| 1 | **Foundation** | 5 | CLAUDE.md, dependency manifest, build scripts, project structure, dep freshness |
| 2 | **Quality Gates** | 11 | Linter, PostToolUse/PreToolUse hooks, pre-commit, CI, error handling, types, coverage |
| 3 | **Intelligence** | 2 | Agent trio (code-reviewer, debugger, architect), domain rules with `paths:` |
| 4 | **Context** | 5 | MCP servers, plugins (context7, episodic-memory), memory files, SessionStart hook |
| 5 | **DX** | 7 | Skills (/test, /status), hook installer, Dependabot, stop hook, unit & smoke tests |

### Severity Levels

The key question: **"Can a real user be harmed by this?"**

| Level | Meaning | Example |
|:------|:--------|:--------|
| :red_circle: **Critical** | Breach risk, data loss | Secrets in git history, `.env` world-readable |
| :orange_circle: **Important** | Code quality, team burden | No pre-commit hooks, no CI |
| :yellow_circle: **Medium** | Nice-to-have improvement | Missing Dependabot, no smoke tests |
| :large_blue_circle: **Minor** | Cosmetic or context-dependent | Missing stop hook, no SessionStart |

### Scoring

```
90%+ = EXCELLENT    Your project is production-ready
70-89% = GOOD       Solid foundation, a few gaps
50-69% = MEDIUM     Needs work — security or quality gaps
<50% = POOR         Significant risks — start with Layer 0
```

## Example Output

### Project Profile (Phase 1)

Before any checks, Doctor profiles your entire project:

```
Project Profile
  Stack:        Python 3.12 / asyncio / PostgreSQL
  Entry Point:  src/main.py
  Test Runner:  pytest, 1089 tests
  Linter:       ruff check + ruff format
  CI/CD:        GitHub Actions
  Deploy:       Railway (Docker)
```

### Finding Format (Phase 3)

Every finding follows the same structure — severity, command, reason, source:

```
🔴 chmod 600 .env .mcp.json
   Secrets are world-readable (644). Any process on the machine can read them.
   → https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html

🟠 Added *.pem *.key *.p12 to .gitignore
   git add . will push private keys to remote. Once in history, removing is painful.
   → https://docs.github.com/en/authentication/keeping-your-account-and-data-secure

🟡 Created scripts/pre-push.sh
   Without pre-push hook, broken code reaches remote. CI catches it 5 min later — too late.
   → https://google.github.io/eng-practices/review/
```

No vague "consider improving security." Every fix has a concrete command, a reason, and a source.

## Installation

### Option A: One command (recommended)

```bash
curl -sSL https://raw.githubusercontent.com/SomeStay07/claude-doctor-skill/main/install.sh | bash
```

### Option B: Manual

```bash
mkdir -p .claude/skills/doctor/layers
cd .claude/skills/doctor

# Main files
curl -sO https://raw.githubusercontent.com/SomeStay07/claude-doctor-skill/main/SKILL.md
curl -sO https://raw.githubusercontent.com/SomeStay07/claude-doctor-skill/main/CHECKLIST.md

# Layer details
cd layers
for f in SECURITY FOUNDATION QUALITY QUALITY-EXTRA INTELLIGENCE CONTEXT DX; do
  curl -sO "https://raw.githubusercontent.com/SomeStay07/claude-doctor-skill/main/layers/$f.md"
done
```

### Verify

```bash
ls .claude/skills/doctor/SKILL.md && echo "Doctor installed"
```

No configuration, API keys, or build step required.

> **Requirements:** [Claude Code](https://docs.anthropic.com/en/docs/claude-code/) CLI installed and a project directory with source code.

## Usage

```bash
# In Claude Code, say:
/doctor              # Full audit — all 6 layers, all 42 checks
/doctor scan         # Diagnose only (phases 1-2, no file changes)
/doctor fix          # Prescribe + apply fixes (phases 3-4)
/doctor layer 0      # Security audit only
/doctor verify       # Health check after fixes (phase 5)

# Or in natural language:
"audit my project"
"check security"
"what's missing in my setup?"
"проверь проект"
"аудит безопасности"
```

## How It Works

```
Phase 1: STUDY        Read project: deps, structure, .env, git, automation
                      Output: Project Profile table

Phase 2: DIAGNOSE     Run 42 checks from CHECKLIST.md
                      Score each layer: X/Y (N%)

Phase 3: PRESCRIBE    For each finding:
                      severity + what to fix + WHY + source link

Phase 4: TREAT        Ask user: "Fix all at once or one by one?"
                      Apply project-specific fixes (not templates)

Phase 5: VERIFY       Run tests, linter, check hooks
                      Output: HEALTH REPORT with total score
```

### Auto-Discovery (DCI)

Doctor automatically detects your stack at startup via Dynamic Context Injection — live shell commands that scan for actual project files:

```
package.json / requirements.txt / Cargo.toml    → stack detection
Makefile / justfile / taskfile.yml               → build system
.claude/ / .mcp.json                              → Claude Code setup
Dockerfile / docker-compose.yml                   → containerization
.github/workflows/ / .gitlab-ci.yml               → CI/CD
```

No configuration needed. Works with 20+ stacks out of the box.

### Built-in Guardrails

<table>
<tr>
<td width="50%" valign="top">

#### Self-Check (7 points)
Before showing results, Doctor validates:
1. Every finding has a WHY?
2. Severity matches reality?
3. No duplicate findings?
4. Fixes are project-specific?
5. Score calculated correctly?
6. N/A checks excluded from score?
7. Sources exist for all claims?

</td>
<td width="50%" valign="top">

#### False Positive Filtering
Doctor **won't flag**:
- Missing CI in hobby projects
- `print()` in CLI scripts
- No Docker for Vercel/serverless
- `.env` 644 on personal Mac (single user)
- Missing MCP if Claude Code not used
- Missing Dependabot if using Nix/Guix
- Missing pre-push if CI runs tests

</td>
</tr>
</table>

#### Error Recovery

| Scenario | What Doctor Does |
|:---------|:-----------------|
| No git repo | Skips git checks, continues with rest |
| No tests | Flags it, doesn't crash |
| No Docker | Skips Docker checks |
| Context overflow | Suggests `/doctor layer <N>` one at a time |
| Check command fails | Logs error, continues with next check |
| Missing tool (ruff, eslint) | Recommends install, doesn't block |

### Incident Response

If Doctor finds secrets in git history, it provides a **9-step recovery plan**:

1. Rotate all exposed credentials immediately
2. Run `git filter-repo` to purge history
3. Force-push cleaned history
4. Invalidate all active sessions
5. Check audit logs for unauthorized access
6. Set up gitleaks pre-commit hook
7. Add CI-level secret scanning
8. Enable GitHub secret scanning
9. Document the incident

Not just "you have a problem" — a complete action plan.

## Multi-Stack Support

Doctor adapts checks, linters, formatters, and SAST tools to whatever stack it finds:

| Stack | Linter | Formatter | Test Runner | SAST |
|:------|:-------|:----------|:------------|:-----|
| Python | ruff | ruff format | pytest | bandit |
| Node.js | eslint | prettier | jest/vitest | eslint-plugin-security |
| TypeScript | eslint + tsc | prettier | jest/vitest | eslint-plugin-security |
| Rust | clippy | rustfmt | cargo test | cargo-audit |
| Go | golangci-lint | gofmt | go test | gosec |
| Ruby | rubocop | rubocop | rspec | brakeman |
| Java | checkstyle | google-java-format | JUnit | SpotBugs |
| PHP | phpstan | php-cs-fixer | PHPUnit | psalm |

Also detects: C/C++, C#, Swift, Kotlin, Scala, Haskell, Elixir, Dart/Flutter, Zig, and more. Build systems: Make, just, npm scripts, Cargo, go mod, Maven, Gradle, Composer, mix, pub, CMake, sbt, cabal, and others.

## Key Design Decisions

### "Project-specific, not templates"

Every fix Doctor generates is tailored to **your** project. A pre-commit hook for a Python/ruff project looks different from one for a TypeScript/eslint project. Doctor reads your actual config files and generates accordingly.

### "Investigate before judging"

Doctor profiles your project (Phase 1) before running any checks (Phase 2). It knows your stack, your test runner, your CI system. Checks that don't apply to your setup are marked N/A and excluded from scoring.

### "Anti-pattern awareness"

Each layer knows specific anti-patterns to avoid:
- **Foundation**: Generic CLAUDE.md rules, code style in markdown
- **Intelligence**: Domain rules without `paths:` waste context
- **Quality**: `except:` without error type = silent failures
- **Context**: Rules >50 lines = Claude ignores them

### "Completion criteria"

An audit isn't done until:
- All 6 layers checked (or marked N/A)
- Each layer has X/Y score
- Total score calculated with grade
- Each finding has severity + why + source
- Concrete fix commands proposed
- User asked "all at once or one by one?"

## Repository Structure

```
claude-doctor-skill/
├── SKILL.md           — Main skill file (entry point for Claude Code)
├── CHECKLIST.md       — Index of all 42 checks across 6 layers
├── layers/
│   ├── SECURITY.md      — Layer 0: 11 security checks + incident response
│   ├── FOUNDATION.md    — Layer 1: 5 foundation checks
│   ├── QUALITY.md       — Layer 2: 7 core quality gate checks
│   ├── QUALITY-EXTRA.md — Layer 2: 4 advanced quality checks
│   ├── INTELLIGENCE.md  — Layer 3: 2 agent intelligence checks
│   ├── CONTEXT.md       — Layer 4: 5 context & memory checks
│   └── DX.md            — Layer 5: 7 developer experience checks
├── assets/
│   ├── logo.svg         — Doctor logo
│   ├── demo-scan.gif    — Animated demo: /doctor scan
│   └── demo-fix.gif     — Animated demo: /doctor fix
├── install.sh         — One-line installer with verification
└── LICENSE
```

One skill. No build step. No dependencies. Install and use.

## Troubleshooting

| Issue | Cause | Fix |
|:------|:------|:----|
| Skill not triggered | File missing or wrong path | Verify `.claude/skills/doctor/SKILL.md` exists |
| Audit is too slow | Very large project | Use `/doctor layer <N>` to audit one layer at a time |
| Context overflow | Too many files to check | Use `/doctor layer <N>` — audit layers individually |
| False positive | Rule doesn't match your setup | Say "this is intentional" — Doctor skips it |
| No output | Older Claude Code version | Run `claude --version` and update to latest |

## See Also

**[Claude Memory Skill](https://github.com/SomeStay07/claude-memory-skill)** — persistent project memory for Claude Code. Remembers decisions, catches contradictions, cleans up stale context. Pairs well with Doctor: memory skill stores conventions, Doctor enforces them.

**[Code Reviewer Agent](https://github.com/SomeStay07/code-review-agent)** — automated code review with concrete fixes. Reviews your diff like a senior engineer — file, line, before/after. Doctor audits the project setup; Code Reviewer audits the code itself.

## Author

Made by [@SomeStay07](https://github.com/SomeStay07) · [Telegram Channel](https://t.me/codeonvibes)

## License

[MIT](LICENSE) — use it, modify it, ship it.
