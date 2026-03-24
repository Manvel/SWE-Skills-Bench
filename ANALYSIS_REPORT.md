# SWE-Skills-Bench: Comprehensive Analysis Report

> **Paper**: SWE-Skills-Bench: Do Agent Skills Actually Help in Real-World Software Engineering?
> **Date**: March 2026
> **Total Skills Analyzed**: 49
> **Total Task Instances**: ~565

---

## Executive Summary

This report provides a detailed analysis of all 49 skills evaluated in the SWE-Skills-Bench paper. The benchmark's core finding is sobering: **skill injection benefits are far more limited than the rapid adoption suggests**.

### Key Metrics at a Glance

| Metric | Value |
|--------|-------|
| **Average Pass Rate Improvement (ΔP)** | +1.2% |
| **Skills with Zero Improvement** | 39 (79.6%) |
| **Skills with Positive Impact** | 7 (14.3%) |
| **Skills with Negative Impact** | 3 (6.1%) |
| **Average Token Overhead** | +10.5% |
| **Token Overhead Range** | -78% to +451% |

---

## Performance Categories

### 1️⃣ ZERO-IMPROVEMENT SKILLS (39 skills, 79.6%)

Skills that produced **ΔP = 0**, meaning skill injection neither helped nor degraded performance.

#### 1.1 Perfect Pass Rate (Both Conditions) — 24 skills

These skills achieved 100% pass rate with AND without the skill, indicating the base model already possessed sufficient capability.

| Rank | Skill Name | Pass Rate | Tokens (w/ skill) | Tokens (w/o skill) | Token Overhead | Analysis |
|------|-----------|-----------|-------------------|-------------------|----------------|----------|
| 1 | [add-uint-support](#add-uint-support) | 100% | 880K | 414K | +112.6% | PyTorch operator support already within base model capability |
| 2 | [analytics-events](#analytics-events) | 100% | 321K | 157K | +104.6% | Event tracking patterns familiar to Claude |
| 3 | [analyze-ci](#analyze-ci) | 100% | 66K | 74K | -10.6% | **Skill reduces tokens**, simpler solution path |
| 4 | [dbt-transformation-patterns](#dbt-transformation-patterns) | 100% | 422K | 208K | +103.2% | DBT already understood by base model |
| 5 | [gitops-workflow](#gitops-workflow) | 100% | 130K | 57K | +127.1% | GitOps concepts standard in modern DevOps |
| 6 | [grafana-dashboards](#grafana-dashboards) | 100% | 150K | 116K | +29.3% | Dashboard configuration patterns well-known |
| 7 | [implementing-agent-modes](#implementing-agent-modes) | 100% | 342K | 655K | **-47.8%** | ⭐ **Skill significantly improves efficiency** |
| 8 | [k8s-manifest-generator](#k8s-manifest-generator) | 100% | 98K | 51K | +91.2% | Kubernetes patterns familiar |
| 9 | [langsmith-fetch](#langsmith-fetch) | 100% | 102K | 97K | +5.9% | LangSmith integration straightforward |
| 10 | [llm-evaluation](#llm-evaluation) | 100% | 238K | 203K | +17.6% | LLM evaluation concepts well-understood |
| 11 | [mcp-builder](#mcp-builder) | 100% | 273K | 200K | +36.1% | MCP patterns standard |
| 12 | [nx-workspace-patterns](#nx-workspace-patterns) | 100% | 417K | 365K | +14.5% | Monorepo patterns well-established |
| 13 | [prometheus-configuration](#prometheus-configuration) | 100% | 225K | 312K | -27.8% | **Skill reduces token usage** |
| 14 | [python-anti-patterns](#python-anti-patterns) | 100% | 274K | 490K | **-44.1%** | ⭐ **Skill significantly improves efficiency** |
| 15 | [python-background-jobs](#python-background-jobs) | 100% | 839K | 249K | +236.8% | Skill creates verbose reasoning path |
| 16 | [python-observability](#python-observability) | 100% | 271K | 105K | +157.5% | Observability patterns already known |
| 17 | [python-packaging](#python-packaging) | 100% | 167K | 74K | +123.9% | Python packaging standard knowledge |
| 18 | [python-performance-optimization](#python-performance-optimization) | 100% | 91K | 96K | -5.1% | **Skill slightly reduces tokens** |
| 19 | [python-resilience](#python-resilience) | 100% | 119K | 529K | **-77.6%** | ⭐⭐ **Highest efficiency gain** |
| 20 | [rag-implementation](#rag-implementation) | 100% | 258K | 179K | +44.5% | RAG patterns well-covered |
| 21 | [service-mesh-observability](#service-mesh-observability) | 100% | 733K | 133K | **+450.8%** | ⚠️ **Massive token overhead**, no correctness gain |
| 22 | [slo-implementation](#slo-implementation) | 100% | 144K | 241K | -40.2% | **Skill reduces tokens** |
| 23 | [spark-optimization](#spark-optimization) | 100% | 223K | 180K | +23.9% | Spark patterns known |
| 24 | [v3-performance-optimization](#v3-performance-optimization) | 100% | 237K | 544K | **-56.4%** | ⭐ **Skill improves efficiency** |

**Key Finding**: Skill injection can drastically increase token consumption (+450.8% for service-mesh-observability) while providing zero correctness benefit. This indicates skills reshape reasoning paths without improving outcomes.

---

#### 1.2 Imperfect Pass Rate (Both Conditions) — 15 skills

These skills show identical pass rates in both conditions, but below 100%. The bottleneck is **capability gap**, not domain knowledge.

| Rank | Skill Name | Pass Rate | Token Overhead | Notes |
|------|-----------|-----------|-----------------|-------|
| 1 | [add-admin-api-endpoint](#add-admin-api-endpoint) | 84.0% | +4.4% | 25 tasks; API endpoint implementation harder than skill covers |
| 2 | [add-malli-schemas](#add-malli-schemas) | 90.0% | +49.2% | Clojure schema complexity beyond skill scope |
| 3 | [bash-defensive-patterns](#bash-defensive-patterns) | 90.9% | +144.3% | Bash defensive coding requires deeper reasoning |
| 4 | [bazel-build-optimization](#bazel-build-optimization) | 90.0% | -60.0% | **Skill reduces tokens** but pass rate unchanged |
| 5 | [changelog-automation](#changelog-automation) | 70.0% | -53.3% | **Skill reduces tokens** for this domain |
| 6 | [clojure-write](#clojure-write) | 81.8% | -33.4% | **Skill reduces tokens**, but Clojure complexity remains |
| 7 | [creating-financial-models](#creating-financial-models) | 90.0% | +0.7% | Financial modeling requires domain expertise beyond skill |
| 8 | [fix](#fix) | 91.7% | +153.0% | ESLint fixing causes excessive reasoning |
| 9 | [github-actions-templates](#github-actions-templates) | 70.0% | +39.1% | Template matching insufficient for complex workflows |
| 10 | [implementing-jsc-classes-zig](#implementing-jsc-classes-zig) | 90.0% | +22.0% | Zig/JSC interop too specialized |
| 11 | [python-configuration](#python-configuration) | 91.7% | +29.7% | Configuration patterns straightforward |
| 12 | [security-review](#security-review) | 92.3% | +0.9% | Security review requires deep reasoning |
| 13 | [turborepo](#turborepo) | 50.0% | +187.9% | ⚠️ Monorepo tools require multi-step reasoning |
| 14 | [vector-index-tuning](#vector-index-tuning) | 90.0% | +18.8% | Vector DB tuning domain-specific |
| 15 | [xlsx](#xlsx) | 36.4% | -18.1% | ⚠️ **Lowest pass rate** — Excel/spreadsheet operations extremely complex |

**Key Finding**: When the base model lacks fundamental capability (e.g., turborepo at 50%, xlsx at 36.4%), skills cannot compensate. The limitation is **reasoning capacity**, not available knowledge.

---

### 2️⃣ POSITIVE-IMPACT SKILLS (7 skills, 14.3%)

Skills that produced **ΔP > 0**, demonstrating meaningful improvement.

| Rank | Skill | Pass+ | Pass- | **ΔP** | Tokens + | Tokens - | **ρ** | **CE** | Category |
|------|-------|-------|-------|--------|----------|----------|--------|--------|----------|
| ⭐⭐ | [risk-metrics-calculation](#risk-metrics-calculation) | 100% | 70% | **+30.0%** | 507K | 778K | **-34.8%** | **-0.86** | **IDEAL** 🎯 |
| ⭐ | [gitlab-ci-patterns](#gitlab-ci-patterns) | 78.6% | 64.3% | **+14.3%** | 326K | 205K | +58.6% | 0.24 | CI/CD |
| | [prompt-engineering-patterns](#prompt-engineering-patterns) | 100% | 90% | **+10.0%** | 218K | 149K | +46.4% | 0.22 | LLM |
| | [similarity-search-patterns](#similarity-search-patterns) | 100% | 90% | **+10.0%** | 144K | 213K | -32.4% | -0.31 | Vector Search |
| | [distributed-tracing](#distributed-tracing) | 100% | 92.3% | **+7.7%** | 115K | 165K | -30.4% | -0.25 | Observability |
| | [tdd-workflow](#tdd-workflow) | 28.6% | 21.4% | **+7.1%** | 148K | 83K | +78.6% | 0.09 | Testing |
| | [istio-traffic-management](#istio-traffic-management) | 100% | 92.9% | **+7.1%** | 95K | 121K | -22.0% | -0.32 | Service Mesh |

#### Detailed Analysis of Positive Performers

##### 🏆 risk-metrics-calculation: The Success Story (+30.0%, ρ = -34.8%)

**Why It Worked**:
- Skill encodes **concrete financial formulas** (Sharpe ratio, max drawdown, VaR, CVaR)
- Domain is **highly specialized** — not common knowledge in general-purpose LLM training
- **Specific, procedural knowledge** that the skill provides (4 pattern classes with 100+ lines of code)
- Agent benefits from **ready-made implementations** rather than deriving formulas

**Token Efficiency**:
- Skill reduces tokens by 34.8% (507K → 778K without)
- Agent follows more direct path when given correct formulas
- **Cost Efficiency (CE = -0.86)**: Best-in-class — performance gain WITH efficiency

**Lesson**: Skills work best when they encode **specialized domain knowledge** not readily available in base model training data.

---

##### gitlab-ci-patterns: Domain-Specific CI/CD (+14.3%, ρ = +58.6%)

**Why It Worked**:
- GitLab CI patterns differ from GitHub Actions (agent's likely reference)
- Skill provides **GitLab-specific YAML syntax** and configuration patterns
- Solves **version-specific challenges** (GitLab API versions, runners)

**Token Impact**: +58.6% overhead, but justified by correctness gain
**Cost Efficiency (CE = 0.24)**: Moderate — performance gain justifies cost

---

##### prompt-engineering-patterns: LLM Domain Knowledge (+10.0%)

**Why It Worked**:
- Prompt engineering is **evolving and subtle** domain
- Base model lacks systematic guidance on structuring prompts for different scenarios
- Skill provides **concrete patterns** (few-shot, chain-of-thought, structured output)

**Token Efficiency**: +46.4% overhead
**Cost Efficiency (CE = 0.22)**: Moderate efficiency

---

#### Summary: When Skills Succeed

✅ **Specialized procedural knowledge** (financial metrics, CI/CD syntax)
✅ **Domain knowledge not commonly in training data** (financial risk, GitLab CI)
✅ **Concrete implementations** rather than abstract guidance
✅ **Skill abstraction level matches task scope** (not too broad, not too narrow)

---

### 3️⃣ NEGATIVE-IMPACT SKILLS (3 skills, 6.1%)

Skills that produced **ΔP < 0**, actively degrading performance through **context interference**.

| Skill | Pass+ | Pass- | **ΔP** | Tokens + | Tokens - | ρ | Issue |
|-------|-------|-------|--------|----------|----------|---|-------|
| [springboot-tdd](#springboot-tdd) | 70.0% | 80.0% | **-10.0%** | 236K | 374K | -36.8% | ⚠️ Over-prescriptive TDD patterns |
| [linkerd-patterns](#linkerd-patterns) | 90.9% | 100.0% | **-9.1%** | 248K | 165K | +50.3% | ⚠️ **Context pollution** (version mismatch) |
| [django-patterns](#django-patterns) | 81.8% | 90.9% | **-9.1%** | 482K | 462K | +4.2% | ⚠️ Over-broad framework guidance |

#### Deep Dive: linkerd-patterns Context Interference (-9.1%)

**The Problem**: A near-miss that triggered catastrophic failure

**Task Requirement**:
```yaml
Create Server CRD + ServerAuthorization CRD for gRPC mTLS
- Use API version v1beta3
- Set proxyProtocol: gRPC
- Configure client.meshTLS.serviceAccounts
```

**Skill Template 5 (Injected)**:
```yaml
apiVersion: policy.linkerd.io/v1beta1  # ❌ Wrong version
kind: Server
proxyProtocol: HTTP/1              # ❌ Wrong protocol
meshTLS:
  unauthenticated: true            # ❌ Wrong auth mode
  networks:
    - cidr: 10.0.0.0/8             # ❌ Unrelated
kind: NetworkPolicy                # ❌ Conflicting resource
```

**Three-Stage Failure Cascade**:

1. **Surface Anchoring** (Stage 1)
   - Agent copied template's v1beta1 + HTTP/1 verbatim
   - Template's concrete values overrode agent's own knowledge
   - Result: Wrong API version for gRPC

2. **Hallucination** (Stage 2)
   - Reconciling mixed authorization modes from template
   - Agent fabricated nonexistent `rules/metricsServers` field
   - Never appeared in any Linkerd CRD version

3. **Concept Bleed** (Stage 3)
   - Template's NetworkPolicy example leaked into solution
   - Agent conflated Linkerd-level auth with Kubernetes-level auth
   - Unrequested resources added to output

**Why Without Skill?** Agent reasoned from first principles:
- ✅ v1beta3 (correct API version)
- ✅ gRPC (correct protocol)
- ✅ Standard client.meshTLS.serviceAccounts (correct auth)
- ✅ No extraneous resources

**Root Cause**: Skill authored as **comprehensive reference** (7 templates covering full stack), but task needed only **narrow slice** → Surplus context created decision pollution.

---

#### springboot-tdd: Over-Prescriptive Checklist (-10.0%)

**Why It Failed**:
- Skill functions as rigid **TDD checklist** that forces edge-case coverage
- When checklist doesn't match task requirements, agent gets confused
- Adds +78.6% token overhead trying to reconcile skill with task
- Eventually fails to deliver correct output (70% vs 80% without skill)

**Token Overhead**: +78.6% (worse reasoning, same failure)

---

#### django-patterns: Scope Mismatch (-9.1%)

**Why It Failed**:
- Skill is **comprehensive Django reference** (734 lines)
- Task is **specific Saleor feature**: low-stock alert with caching
- Surplus guidance on Django project structure, DRF patterns, signals, etc.
- Agent gets distracted by **too many possible approaches**

**Issue**: Holistic scope vs. focused requirement

---

#### Summary: Why Skills Fail

❌ **Context pollution**: Near-matches with wrong concrete values
❌ **Over-breadth**: Comprehensive guidance when narrow solution needed
❌ **Version mismatches**: Template encodes outdated/wrong API versions
❌ **Decision space expansion**: Surplus patterns cause agent confusion
❌ **Concept bleed**: Related domains leak into unrelated tasks

---

## Detailed Skill Analysis

### Alphabetical Skill Breakdown

#### add-admin-api-endpoint
- **Links**: [📄 View Skill](skills/add-admin-api-endpoint/SKILL.md) | [📋 View Task](tasks/add-admin-api-endpoint.md) | [🔗 GitHub](https://github.com/TryGhost/Ghost)
- **Category**: API Development (Zero Improvement)
- **Pass Rate**: 84.0% (both with/without skill)
- **Token Overhead**: +4.4% (minimal)
- **Analysis**: Adding admin API endpoints requires understanding of auth, permissions, serialization, and testing. Base model already handles this well. Skill provides structure but doesn't improve correctness. 25 instances suggest API complexity varies; skill doesn't address all patterns.
- **Recommendation**: Skill could be improved by including authentication/authorization patterns specific to admin endpoints.

---

#### add-malli-schemas
- **Links**: [📄 View Skill](skills/add-malli-schemas/SKILL.md) | [📋 View Task](tasks/add-malli-schemas.md) | [🔗 GitHub](https://github.com/metabase/metabase)
- **Category**: API Development (Zero Improvement)
- **Pass Rate**: 90.0% (both conditions)
- **Token Overhead**: +49.2%
- **Analysis**: Malli is a Clojure schema library. 90% pass rate indicates good baseline capability. Token overhead suggests skill introduces verbose reasoning without correctness benefit.
- **Recommendation**: The 10% failure likely stems from Clojure language complexity, not schema patterns.

---

#### add-uint-support
- **Links**: [📄 View Skill](skills/add-uint-support/SKILL.md) | [📋 View Task](tasks/add-uint-support.md)
- **Category**: Developer Tools (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +112.6%
- **Analysis**: PyTorch operator support for uint32/uint64. Base model sufficiently understands type systems and operator dispatch. Skill doubles token usage without improving correctness.
- **Recommendation**: PyTorch knowledge is well-represented in training data; skill adds redundancy.

---

#### analytics-events
- **Links**: [📄 View Skill](skills/analytics-events/SKILL.md) | [📋 View Task](tasks/analytics-events.md) | [🔗 GitHub](https://github.com/metabase/metabase)
- **Category**: Analytics & Monitoring (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +104.6%
- **Analysis**: Event tracking and analytics patterns are standard in modern software development. Base model handles well; skill causes verbose reasoning.
- **Recommendation**: Generic skill; base model sufficient.

---

#### analyze-ci
- **Links**: [📄 View Skill](skills/analyze-ci/SKILL.md) | [📋 View Task](tasks/analyze-ci.md) | [🔗 GitHub](https://github.com/getsentry/sentry)
- **Category**: Analytics & Monitoring (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: -10.6% ✅ **SKILL REDUCES TOKENS**
- **Analysis**: CI analysis skill actually makes agent more efficient! The skill must provide a direct solution path that avoids unnecessary exploration.
- **Recommendation**: This is a well-designed skill — maintains correctness while reducing cognitive overhead.

---

#### bash-defensive-patterns
- **Links**: [📄 View Skill](skills/bash-defensive-patterns/SKILL.md) | [📋 View Task](tasks/bash-defensive-patterns.md) | [🔗 GitHub](https://github.com/koalaman/shellcheck)
- **Category**: Security & Testing (Zero Improvement - Imperfect)
- **Pass Rate**: 90.9% (both conditions)
- **Token Overhead**: +144.3%
- **Analysis**: Defensive bash programming (error handling, input validation, robustness). 90.9% pass rate indicates some complex cases fail. Skill adds 144% tokens without helping.
- **Recommendation**: The 9.1% failures likely require deep bash knowledge beyond what skill provides.

---

#### bazel-build-optimization
- **Links**: [📄 View Skill](skills/bazel-build-optimization/SKILL.md) | [📋 View Task](tasks/bazel-build-optimization.md) | [🔗 GitHub](https://github.com/bazelbuild/bazel)
- **Category**: Developer Tools (Zero Improvement - Imperfect)
- **Pass Rate**: 90.0% (both conditions)
- **Token Overhead**: -60.0% ✅ **SKILL REDUCES TOKENS SIGNIFICANTLY**
- **Analysis**: Bazel is complex build system. Skill guides agent to efficient solution path despite not improving pass rate.
- **Recommendation**: Well-designed skill — token efficiency suggests good pedagogical structure.

---

#### changelog-automation
- **Links**: [📄 View Skill](skills/changelog-automation/SKILL.md) | [📋 View Task](tasks/changelog-automation.md) | [🔗 GitHub](https://github.com/github-changelog-generator/github-changelog-generator)
- **Category**: Developer Tools (Zero Improvement - Imperfect)
- **Pass Rate**: 70.0% (both conditions)
- **Token Overhead**: -53.3% ✅ **SKILL REDUCES TOKENS**
- **Analysis**: Changelog generation is relatively straightforward. 70% pass suggests some edge cases in formatting/structure. Skill reduces tokens by helping agent find quick path (even though pass rate unchanged).
- **Recommendation**: Skill could be enhanced to cover edge cases causing the 30% failure.

---

#### clojure-write
- **Links**: [📄 View Skill](skills/clojure-write/SKILL.md) | [📋 View Task](tasks/clojure-write.md) | [🔗 GitHub](https://github.com/metabase/metabase)
- **Category**: Developer Tools (Zero Improvement - Imperfect)
- **Pass Rate**: 81.8% (both conditions)
- **Token Overhead**: -33.4% ✅ **SKILL REDUCES TOKENS**
- **Analysis**: Clojure language fundamentals. 81.8% suggests Clojure unfamiliarity in base model. Skill efficiently guides toward solutions but doesn't overcome language barrier.
- **Recommendation**: Skill is well-designed for efficiency; the 18.2% gap is likely Clojure language complexity.

---

#### creating-financial-models
- **Links**: [📄 View Skill](skills/creating-financial-models/SKILL.md) | [📋 View Task](tasks/creating-financial-models.md) | [🔗 GitHub](https://github.com/lballabio/QuantLib)
- **Category**: Data Science & ML (Zero Improvement - Imperfect)
- **Pass Rate**: 90.0% (both conditions)
- **Token Overhead**: +0.7% (negligible)
- **Analysis**: Financial modeling requires domain expertise. 90% suggests basic modeling works; edge cases fail. Skill adds no tokens yet provides no improvement.
- **Recommendation**: Skill is minimal/ineffectual. Consider enhancing with financial concepts (present value, NPV, risk metrics).

---

#### dbt-transformation-patterns
- **Links**: [📄 View Skill](skills/dbt-transformation-patterns/SKILL.md) | [📋 View Task](tasks/dbt-transformation-patterns.md) | [🔗 GitHub](https://github.com/dbt-labs/dbt-core)
- **Category**: Data Science & ML (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +103.2%
- **Analysis**: dbt (data build tool) patterns. Base model understands transformation pipelines; skill adds verbose reasoning.
- **Recommendation**: dbt is well-understood; skill is redundant.

---

#### distributed-tracing
- **Links**: [📄 View Skill](skills/distributed-tracing/SKILL.md) | [📋 View Task](tasks/distributed-tracing.md) | [🔗 GitHub](https://github.com/open-telemetry/opentelemetry-collector)
- **Category**: Analytics & Monitoring (Positive Impact ✅)
- **Pass Rate**: +7.7% (92.3% → 100%)
- **Token Overhead**: -30.4% ✅ **SKILL REDUCES TOKENS**
- **Analysis**: Distributed tracing (OpenTelemetry, spans, context propagation) is specialized domain. Skill effectively guides to correct implementation with better efficiency.
- **Recommendation**: Great skill design — specialized knowledge, proper abstraction level.

---

#### django-patterns
- **Links**: [📄 View Skill](skills/django-patterns/SKILL.md) | [📋 View Task](tasks/django-patterns.md) | [🔗 GitHub](https://github.com/saleor/saleor)
- **Category**: API Development (Negative Impact ❌)
- **Pass Rate**: -9.1% (90.9% → 81.8%)
- **Token Overhead**: +4.2%
- **Analysis**: Comprehensive Django patterns (734 lines). Task requires low-stock alert feature with caching. Skill's breadth (project structure, DRF, ORM, signals, middleware, etc.) creates decision confusion. Agent struggles to apply specific guidance to focused task.
- **Recommendation**: Split skill into targeted sub-skills (e.g., "django-signals-patterns", "django-caching-patterns") for focused application.
- **Paper Insight**: "Surplus context can interfere with agent's reasoning in several ways... unnecessarily expands decision space."

---

#### fix
- **Links**: [📄 View Skill](skills/fix/SKILL.md) | [📋 View Task](tasks/fix.md) | [🔗 GitHub](https://github.com/michaelasper/upgradle/tree/5f292188e9b427a96d3573b29e5677e4cdce58ea) @ `5f292188`
- **Category**: Developer Tools (Zero Improvement - Imperfect)
- **Pass Rate**: 91.7% (both conditions)
- **Token Overhead**: +153.0%
- **Analysis**: Linting and code fixing (ESLint, Prettier). 91.7% is decent; 8.3% failures are edge-case lint rules. Skill adds 153% tokens — verbose reasoning without correctness gain.
- **Recommendation**: Skill could be simplified to focus on top-3 most common lint errors.

---

#### github-actions-templates
- **Links**: [📄 View Skill](skills/github-actions-templates/SKILL.md) | [📋 View Task](tasks/github-actions-templates.md) | [🔗 GitHub](https://github.com/actions/starter-workflows)
- **Category**: Deployment & DevOps (Zero Improvement - Imperfect)
- **Pass Rate**: 70.0% (both conditions)
- **Token Overhead**: +39.1%
- **Analysis**: GitHub Actions workflow templates. 70% suggests complex automation patterns fail. Skill adds overhead without helping. Base model struggles with YAML structure/logic.
- **Recommendation**: Improve with example workflows for common patterns (CI/CD, testing, deployment).

---

#### gitops-workflow
- **Links**: [📄 View Skill](skills/gitops-workflow/SKILL.md) | [📋 View Task](tasks/gitops-workflow.md) | [🔗 GitHub](https://github.com/fluxcd/flux2)
- **Category**: Deployment & DevOps (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +127.1%
- **Analysis**: GitOps patterns (declarative IaC, reconciliation loops). Base model handles well; skill creates verbose path.
- **Recommendation**: Well-understood domain; skill is redundant.

---

#### gitlab-ci-patterns
- **Links**: [📄 View Skill](skills/gitlab-ci-patterns/SKILL.md) | [📋 View Task](tasks/gitlab-ci-patterns.md) | [🔗 GitHub](https://github.com/gitlabhq/gitlabhq)
- **Category**: Deployment & DevOps (Positive Impact ✅)
- **Pass Rate**: +14.3% (64.3% → 78.6%)
- **Token Overhead**: +58.6%
- **Analysis**: GitLab CI/CD patterns (different from GitHub Actions). Skill provides **GitLab-specific YAML syntax, runners, variables**. This specialized knowledge isn't in base model's standard training. Agent uses more tokens but achieves higher correctness.
- **Cost Efficiency (CE = 0.24)**: Good — performance gain justifies overhead.
- **Recommendation**: Excellent skill. Demonstrates that **domain-specific knowledge** drives improvement.

---

#### grafana-dashboards
- **Links**: [📄 View Skill](skills/grafana-dashboards/SKILL.md) | [📋 View Task](tasks/grafana-dashboards.md) | [🔗 GitHub](https://github.com/grafana/grafana)
- **Category**: Analytics & Monitoring (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +29.3%
- **Analysis**: Grafana dashboard JSON configuration. Base model handles JSON generation well. Skill adds modest overhead.
- **Recommendation**: Base model sufficient for generic dashboards; skill not needed.

---

#### implementing-agent-modes
- **Links**: [📄 View Skill](skills/implementing-agent-modes/SKILL.md) | [📋 View Task](tasks/implementing-agent-modes.md) | [🔗 GitHub](https://github.com/PostHog/posthog)
- **Category**: Developer Tools (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: -47.8% ✅ **SKILL SIGNIFICANTLY REDUCES TOKENS**
- **Analysis**: Agent mode implementation (likely LLM agent patterns). Skill effectively guides to efficient solution path. Agent goes from 655K to 342K tokens (47.8% savings).
- **Recommendation**: Well-designed skill. Good balance of structure and guidance.

---

#### implementing-jsc-classes-zig
- **Links**: [📄 View Skill](skills/implementing-jsc-classes-zig/SKILL.md) | [📋 View Task](tasks/implementing-jsc-classes-zig.md) | [🔗 GitHub](https://github.com/oven-sh/bun)
- **Category**: Developer Tools (Zero Improvement - Imperfect)
- **Pass Rate**: 90.0% (both conditions)
- **Token Overhead**: +22.0%
- **Analysis**: Zig language with JavaScript class interop. 90% suggests most patterns work; edge cases fail. Zig is obscure language; 10% gap likely due to language unfamiliarity, not skill quality.
- **Recommendation**: Skill could include more JSC API documentation.

---

#### istio-traffic-management
- **Links**: [📄 View Skill](skills/istio-traffic-management/SKILL.md) | [📋 View Task](tasks/istio-traffic-management.md) | [🔗 GitHub](https://github.com/istio/istio)
- **Category**: Deployment & DevOps (Positive Impact ✅)
- **Pass Rate**: +7.1% (92.9% → 100%)
- **Token Overhead**: -22.0% ✅ **SKILL REDUCES TOKENS**
- **Analysis**: Istio service mesh configuration. Skill provides **traffic management patterns** (virtual services, destination rules) that aren't trivial. High pass rate with skill + lower tokens = excellent design.
- **Recommendation**: Strong skill for specialized service mesh domain.

---

#### k8s-manifest-generator
- **Links**: [📄 View Skill](skills/k8s-manifest-generator/SKILL.md) | [📋 View Task](tasks/k8s-manifest-generator.md) | [🔗 GitHub](https://github.com/kubernetes-sigs/kustomize)
- **Category**: Deployment & DevOps (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +91.2%
- **Analysis**: Kubernetes YAML generation. Base model generates valid K8s manifests well. Skill adds overhead.
- **Recommendation**: Base model sufficient.

---

#### langsmith-fetch
- **Links**: [📄 View Skill](skills/langsmith-fetch/SKILL.md) | [📋 View Task](tasks/langsmith-fetch.md) | [🔗 GitHub](https://github.com/langchain-ai/langchain)
- **Category**: Developer Tools (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +5.9% (minimal)
- **Analysis**: LangSmith API integration. Base model handles API calls well. Skill adds minimal overhead.
- **Recommendation**: Well-balanced skill — not redundant, not verbose.

---

#### linkerd-patterns
- **Links**: [📄 View Skill](skills/linkerd-patterns/SKILL.md) | [📋 View Task](tasks/linkerd-patterns.md) | [🔗 GitHub](https://github.com/linkerd/linkerd2)
- **Category**: Deployment & DevOps (Negative Impact ❌)
- **Pass Rate**: -9.1% (100% → 90.9%)
- **Token Overhead**: +50.3%
- **Analysis**: **CRITICAL CASE STUDY** — Context interference from near-miss template. See detailed analysis in Section 3 above. Wrong API versions, hallucinated fields, concept bleed.
- **Recommendation**: Redesign skill to provide abstract guidance (e.g., "Use latest API version available in your cluster") rather than concrete templates with hard-coded values.
- **Paper Insight**: "Skill design should favor abstract guidance patterns over concrete, opinionated templates."

---

#### llm-evaluation
- **Links**: [📄 View Skill](skills/llm-evaluation/SKILL.md) | [📋 View Task](tasks/llm-evaluation.md) | [🔗 GitHub](https://github.com/stanford-crfm/helm)
- **Category**: Data Science & ML (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +17.6%
- **Analysis**: LLM evaluation metrics and frameworks. Base model understands evaluation; skill adds guidance but not essential.
- **Recommendation**: Skill provides good structure for common evaluation scenarios.

---

#### mcp-builder
- **Links**: [📄 View Skill](skills/mcp-builder/SKILL.md) | [📋 View Task](tasks/mcp-builder.md) | [🔗 GitHub](https://github.com/modelcontextprotocol/servers)
- **Category**: Developer Tools (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +36.1%
- **Analysis**: MCP (Model Context Protocol) builder. Base model handles protocol implementation; skill is supportive.
- **Recommendation**: Reasonable skill for specialized protocol.

---

#### nx-workspace-patterns
- **Links**: [📄 View Skill](skills/nx-workspace-patterns/SKILL.md) | [📋 View Task](tasks/nx-workspace-patterns.md) | [🔗 GitHub](https://github.com/nrwl/nx)
- **Category**: Developer Tools (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +14.5%
- **Analysis**: Nx monorepo patterns. Base model understands monorepo structures. Skill adds modest overhead.
- **Recommendation**: Well-balanced skill.

---

#### prometheus-configuration
- **Links**: [📄 View Skill](skills/prometheus-configuration/SKILL.md) | [📋 View Task](tasks/prometheus-configuration.md) | [🔗 GitHub](https://github.com/prometheus/prometheus)
- **Category**: Analytics & Monitoring (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: -27.8% ✅ **SKILL REDUCES TOKENS**
- **Analysis**: Prometheus config (scrape jobs, alerting rules). Skill guides to efficient configuration despite perfect pass rate in both conditions.
- **Recommendation**: Well-designed skill for Prometheus configurations.

---

#### prompt-engineering-patterns
- **Links**: [📄 View Skill](skills/prompt-engineering-patterns/SKILL.md) | [📋 View Task](tasks/prompt-engineering-patterns.md) | [🔗 GitHub](https://github.com/langchain-ai/langchain)
- **Category**: LLM (Positive Impact ✅)
- **Pass Rate**: +10.0% (90% → 100%)
- **Token Overhead**: +46.4%
- **Analysis**: Prompt engineering is evolving domain (few-shot, chain-of-thought, structured output). Skill provides systematic guidance. Correctness improves to 100% with skill.
- **Cost Efficiency (CE = 0.22)**: Good.
- **Recommendation**: Strong skill. Demonstrates structured prompt patterns drive improvement.

---

#### python-anti-patterns
- **Links**: [📄 View Skill](skills/python-anti-patterns/SKILL.md) | [📋 View Task](tasks/python-anti-patterns.md) | [🔗 GitHub](https://github.com/mahmoud/boltons)
- **Category**: Developer Tools (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: -44.1% ✅ **SKILL SIGNIFICANTLY REDUCES TOKENS**
- **Analysis**: Python anti-patterns identification and avoidance. Base model already knows; skill guides to **efficient code path** (490K → 274K tokens = 44% reduction).
- **Recommendation**: Excellent skill — maintains correctness while optimizing reasoning.

---

#### python-background-jobs
- **Links**: [📄 View Skill](skills/python-background-jobs/SKILL.md) | [📋 View Task](tasks/python-background-jobs.md) | [🔗 GitHub](https://github.com/celery/celery)
- **Category**: Data Science & ML (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +236.8% ⚠️ **MASSIVE OVERHEAD**
- **Analysis**: Background job patterns (Celery, task queues). Perfect pass rate in both conditions. But skill causes agent to use 3.4x more tokens (249K → 839K).
- **Recommendation**: Skill creates unnecessary complexity. Simplify to direct job queue patterns.

---

#### python-configuration
- **Links**: [📄 View Skill](skills/python-configuration/SKILL.md) | [📋 View Task](tasks/python-configuration.md) | [🔗 GitHub](https://github.com/fastapi/fastapi)
- **Category**: Data Science & ML (Zero Improvement - Imperfect)
- **Pass Rate**: 91.7% (both conditions)
- **Token Overhead**: +29.7%
- **Analysis**: Python configuration management (env vars, config files, secrets). 91.7% suggests straightforward patterns. Skill adds overhead.
- **Recommendation**: Most config patterns are standard; skill could be trimmed.

---

#### python-observability
- **Links**: [📄 View Skill](skills/python-observability/SKILL.md) | [📋 View Task](tasks/python-observability.md) | [🔗 GitHub](https://github.com/open-telemetry/opentelemetry-python)
- **Category**: Analytics & Monitoring (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +157.5%
- **Analysis**: Python logging, tracing, metrics. Base model handles well; skill causes excessive reasoning (105K → 271K tokens).
- **Recommendation**: Trim skill to focus on most common observability patterns.

---

#### python-packaging
- **Links**: [📄 View Skill](skills/python-packaging/SKILL.md) | [📋 View Task](tasks/python-packaging.md) | [🔗 GitHub](https://github.com/pypa/packaging)
- **Category**: Developer Tools (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +123.9%
- **Analysis**: Python package distribution (setuptools, wheels, PyPI). Standard knowledge; skill adds overhead.
- **Recommendation**: Base model sufficient.

---

#### python-performance-optimization
- **Links**: [📄 View Skill](skills/python-performance-optimization/SKILL.md) | [📋 View Task](tasks/python-performance-optimization.md) | [🔗 GitHub](https://github.com/benfred/py-spy)
- **Category**: Developer Tools (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: -5.1% ✅ **SKILL SLIGHTLY REDUCES TOKENS**
- **Analysis**: Python performance techniques (profiling, optimization). Base model handles; skill slightly improves efficiency.
- **Recommendation**: Good, concise skill.

---

#### python-resilience
- **Links**: [📄 View Skill](skills/python-resilience/SKILL.md) | [📋 View Task](tasks/python-resilience.md) | [🔗 GitHub](https://github.com/encode/httpx)
- **Category**: Deployment & DevOps (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: -77.6% ✅ **HIGHEST EFFICIENCY GAIN**
- **Analysis**: Python resilience patterns (retries, timeouts, circuit breakers). Base model understands; skill guides to **extremely efficient path** (529K → 119K tokens = 77.6% reduction).
- **Recommendation**: ⭐ **EXCELLENT SKILL DESIGN** — Provides clear structure that agent leverages for efficiency without sacrificing correctness.

---

#### rag-implementation
- **Links**: [📄 View Skill](skills/rag-implementation/SKILL.md) | [📋 View Task](tasks/rag-implementation.md) | [🔗 GitHub](https://github.com/langchain-ai/langchain)
- **Category**: Data Science & ML (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +44.5%
- **Analysis**: Retrieval-Augmented Generation. Base model understands RAG; skill adds supportive guidance.
- **Recommendation**: Reasonable skill for RAG patterns.

---

#### risk-metrics-calculation
- **Links**: [📄 View Skill](skills/risk-metrics-calculation/SKILL.md) | [📋 View Task](tasks/risk-metrics-calculation.md) | [🔗 GitHub](https://github.com/quantopian/pyfolio)
- **Category**: Data Science & ML (Positive Impact ✅⭐⭐)
- **Pass Rate**: +30.0% (70% → 100%)
- **Token Overhead**: -34.8% ✅ **SKILL REDUCES TOKENS**
- **Analysis**: **BEST PERFORMER** — Risk metrics (Sharpe, max drawdown, VaR, CVaR) are specialized, not trivial. Skill provides **concrete formulas and implementations** (500+ lines of financial code). Agent goes from 70% → 100% correctness while reducing tokens by 35%.
- **Cost Efficiency (CE = -0.86)**: Best-in-class.
- **Recommendation**: ⭐⭐ **GOLD STANDARD SKILL** — Demonstrates what skill injection can achieve: specialized knowledge + concrete implementation + improved efficiency.
- **Key Insight**: Financial domain not well-covered in base model; skill fills critical gap with proven formulas.

---

#### security-review
- **Links**: [📄 View Skill](skills/security-review/SKILL.md) | [📋 View Task](tasks/security-review.md) | [🔗 GitHub](https://github.com/babybuddy/babybuddy)
- **Category**: Security & Testing (Zero Improvement - Imperfect)
- **Pass Rate**: 92.3% (both conditions)
- **Token Overhead**: +0.9% (negligible)
- **Analysis**: Security review guidance. 92.3% is strong. 7.7% failures likely require deep security expertise beyond skill scope.
- **Recommendation**: Skill is efficient; the gap isn't due to overhead.

---

#### service-mesh-observability
- **Links**: [📄 View Skill](skills/service-mesh-observability/SKILL.md) | [📋 View Task](tasks/service-mesh-observability.md) | [🔗 GitHub](https://github.com/linkerd/linkerd2)
- **Category**: Analytics & Monitoring (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +450.8% ⚠️⚠️⚠️ **EXTREME OVERHEAD**
- **Analysis**: **WORST CASE** — Service mesh observability. Perfect correctness in both conditions. But skill causes **4.5x token increase** (133K → 733K). Agent reasoning becomes extremely verbose for task already solvable by base model.
- **Recommendation**: ❌ **SKILL SHOULD BE DEPRECATED** — Provides no correctness gain while incurring massive overhead. Redesign or remove.

---

#### similarity-search-patterns
- **Links**: [📄 View Skill](skills/similarity-search-patterns/SKILL.md) | [📋 View Task](tasks/similarity-search-patterns.md) | [🔗 GitHub](https://github.com/milvus-io/milvus)
- **Category**: Data Science & ML (Positive Impact ✅)
- **Pass Rate**: +10.0% (90% → 100%)
- **Token Overhead**: -32.4% ✅ **SKILL REDUCES TOKENS**
- **Analysis**: Vector similarity search (embeddings, indexing, ranking). Skill guides to correct patterns with improved efficiency. Pass rate improves to 100% while reducing tokens.
- **Cost Efficiency (CE = -0.31)**: Reasonable.
- **Recommendation**: Good skill for vector search domain.

---

#### slo-implementation
- **Links**: [📄 View Skill](skills/slo-implementation/SKILL.md) | [📋 View Task](tasks/slo-implementation.md) | [🔗 GitHub](https://github.com/google/slo-generator)
- **Category**: Analytics & Monitoring (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: -40.2% ✅ **SKILL REDUCES TOKENS**
- **Analysis**: Service Level Objective (SLO) implementation. Base model handles; skill guides to efficient path (241K → 144K tokens).
- **Recommendation**: Well-designed skill.

---

#### spark-optimization
- **Links**: [📄 View Skill](skills/spark-optimization/SKILL.md) | [📋 View Task](tasks/spark-optimization.md) | [🔗 GitHub](https://github.com/apache/spark)
- **Category**: Data Science & ML (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: +23.9%
- **Analysis**: Apache Spark performance optimization. Base model understands Spark; skill adds modest guidance.
- **Recommendation**: Reasonable skill.

---

#### springboot-tdd
- **Links**: [📄 View Skill](skills/springboot-tdd/SKILL.md) | [📋 View Task](tasks/springboot-tdd.md) | [🔗 GitHub](https://github.com/spring-projects/spring-petclinic)
- **Category**: Security & Testing (Negative Impact ❌)
- **Pass Rate**: -10.0% (80% → 70%)
- **Token Overhead**: -36.8% ✅ **SKILL REDUCES TOKENS**
- **Analysis**: Spring Boot TDD patterns. Skill causes **correctness degradation** (80% → 70%) despite reducing tokens. Over-prescriptive TDD checklist constrains agent flexibility. When skill's checklist doesn't match task requirements, agent fails.
- **Recommendation**: Redesign skill to provide flexible guidance rather than rigid checklist.

---

#### tdd-workflow
- **Links**: [📄 View Skill](skills/tdd-workflow/SKILL.md) | [📋 View Task](tasks/tdd-workflow.md) | [🔗 GitHub](https://github.com/tdd-starters/python)
- **Category**: Security & Testing (Positive Impact ✅)
- **Pass Rate**: +7.1% (21.4% → 28.6%)
- **Token Overhead**: +78.6% ⚠️
- **Analysis**: TDD workflow structure. Task is inherently hard (21.4% baseline). Skill improves to 28.6% (+7.1%). Token overhead is high (+78.6%), suggesting agent explores many verification paths per test. But gain is positive.
- **Cost Efficiency (CE = 0.09)**: Low efficiency — gains don't justify overhead.
- **Recommendation**: Skill helps but expensive. Consider optimizing token usage.

---

#### turborepo
- **Links**: [📄 View Skill](skills/turborepo/SKILL.md) | [📋 View Task](tasks/turborepo.md) | [🔗 GitHub](https://github.com/vercel/turbo)
- **Category**: Developer Tools (Zero Improvement - Imperfect)
- **Pass Rate**: 50.0% (both conditions)
- **Token Overhead**: +187.9% ⚠️
- **Analysis**: Turborepo monorepo tooling. **Lowest success rate after xlsx (50%)**. Skill adds 187% tokens without improving correctness. Monorepo configuration is complex; base model struggles fundamentally.
- **Recommendation**: Task may be too hard for current models. Skill needs fundamental redesign to address root causes.

---

#### v3-performance-optimization
- **Links**: [📄 View Skill](skills/v3-performance-optimization/SKILL.md) | [📋 View Task](tasks/v3-performance-optimization.md) | [🔗 GitHub](https://github.com/Dao-AILab/flash-attention)
- **Category**: Developer Tools (Zero Improvement - Perfect Pass)
- **Pass Rate**: 100% (both conditions)
- **Token Overhead**: -56.4% ✅ **SKILL SIGNIFICANTLY REDUCES TOKENS**
- **Analysis**: v3 framework performance optimization. Base model handles; skill provides efficient guidance path (544K → 237K tokens).
- **Recommendation**: Excellent skill — clear guidance with efficiency gains.

---

#### vector-index-tuning
- **Links**: [📄 View Skill](skills/vector-index-tuning/SKILL.md) | [📋 View Task](tasks/vector-index-tuning.md) | [🔗 GitHub](https://github.com/facebookresearch/faiss)
- **Category**: Data Science & ML (Zero Improvement - Imperfect)
- **Pass Rate**: 90.0% (both conditions)
- **Token Overhead**: +18.8%
- **Analysis**: Vector index optimization (vector DBs, indexing strategies). 90% suggests core patterns work. 10% failures likely edge cases in tuning parameters.
- **Recommendation**: Skill could enhance with parameter tuning heuristics.

---

#### xlsx
- **Links**: [📄 View Skill](skills/xlsx/SKILL.md) | [📋 View Task](tasks/xlsx.md) | [🔗 GitHub](https://github.com/ericgazoni/openpyxl)
- **Category**: Analytics & Monitoring (Zero Improvement - Imperfect)
- **Pass Rate**: 36.4% (both conditions)
- **Token Overhead**: -18.1%
- **Analysis**: **LOWEST SUCCESS RATE ACROSS BENCHMARK** (36.4%). Excel/spreadsheet operations are surprisingly complex. Skill reduces tokens slightly but cannot overcome fundamental capability gap.
- **Recommendation**: Task may exceed model capabilities. Consider breaking into smaller tasks.

---

---

## Key Findings Summary

### Finding 1: Skill Injection Yields Limited Marginal Gains

**Result**: 39 of 49 skills (79.6%) produce **ΔP = 0** (zero improvement)

**Why**:
- 24 skills: Base model already achieves 100% pass rate (domain already understood)
- 15 skills: Pass rates identical but imperfect; **bottleneck is capability, not knowledge**

**Implication**: Skills are **not a universal performance booster**. They're a targeted intervention whose utility depends entirely on domain fit.

---

### Finding 2: Token Overhead Decoupled from Correctness

**Result**: ρ (token overhead) ranges from -78% to +451% with **no correlation to ΔP**

**Examples**:
- service-mesh-observability: +450.8% overhead, 0% improvement
- python-resilience: -77.6% overhead, 0% improvement
- risk-metrics-calculation: -34.8% overhead, +30% improvement

**Implication**: Skills reshape reasoning paths independently of correctness outcomes. A skill can make agent verbose without helping, or concise without hurting.

---

### Finding 3: Seven Specialized Skills Deliver Meaningful Gains

**Results**: 7 skills show ΔP > 0 (ranging +7.1% to +30.0%)

**Common Patterns**:
- ✅ **Specialized domain knowledge** (financial metrics, GitLab CI, distributed tracing)
- ✅ **Knowledge not in base model training** (risk formulas, GitLab-specific YAML)
- ✅ **Concrete implementations** (code/patterns rather than abstract guidance)
- ✅ **Proper abstraction level** (scoped to task domain, not over-broad)

**Best Performers**:
1. risk-metrics-calculation (+30.0%, -34.8% tokens)
2. gitlab-ci-patterns (+14.3%, +58.6% tokens)
3. prompt-engineering-patterns (+10.0%, +46.4% tokens)

---

### Finding 4: Three Skills Actively Degrade Performance

**Results**: 3 skills show ΔP < 0 (ranging -10.0% to -9.1%)

**Root Causes**:

| Skill | Issue | Mechanism |
|-------|-------|-----------|
| linkerd-patterns | Version-mismatched templates | Surface anchoring + hallucination + concept bleed |
| springboot-tdd | Over-prescriptive checklist | Rigid TDD constraints vs. task flexibility |
| django-patterns | Over-broad guidance | Surplus patterns expand decision space |

**Lesson**: Skill injection carries **structural risk of context interference**. Near-matches with wrong concrete values trigger cascading failures.

---

## Design Principles for Effective Skills

Based on paper findings and analysis:

### ✅ DO:

1. **Encode specialized domain knowledge** not in base model training data
   - Example: risk-metrics-calculation (financial formulas)
   - Example: gitlab-ci-patterns (GitLab-specific syntax)

2. **Provide concrete implementations**
   - Example: RiskMetrics class with 500+ lines of code
   - Example: Concrete CI/CD YAML patterns
   - **Not**: Abstract guidance that requires interpretation

3. **Match abstraction level to task scope**
   - Example: istio-traffic-management (focused service mesh patterns)
   - **Not**: django-patterns (734-line comprehensive reference)

4. **Use abstract guidance for patterns, not hard-coded values**
   - Example: "Use latest available API version" > "Use v1beta3"
   - Prevents surface anchoring on outdated concrete examples

5. **Validate against recent framework versions**
   - Ensure code examples work with current APIs
   - linkerd-patterns failed because templates used v1beta1 vs. v1beta3

### ❌ DON'T:

1. **Create redundant skills for well-known domains**
   - Example: python-packaging (standard knowledge)
   - Adds overhead without correctness gain

2. **Over-broaden skill scope**
   - Example: django-patterns (734 lines for specific low-stock alert task)
   - Creates decision pollution

3. **Hard-code concrete parameter values**
   - Example: linkerd-patterns Template 5 with v1beta1 + HTTP/1
   - Triggers surface anchoring when task requires different values

4. **Mix unrelated domains**
   - Example: linkerd-patterns' NetworkPolicy confusing K8s and Linkerd concepts
   - Causes concept bleed

5. **Create rigid, checklist-style guidance**
   - Example: springboot-tdd's TDD constraints
   - Reduces flexibility for task variations

---

## Recommendations for Practitioners

### For Users (When to Use Skills)

✅ **Use skills for**:
- Specialized domains (financial modeling, service mesh, GitLab CI)
- Knowledge gaps in base model
- Tasks where you've verified skill improves correctness
- Domains with recent/evolving best practices

❌ **Avoid skills for**:
- Well-understood domains (Python basics, JSON generation)
- Tasks where base model achieves 100% success rate
- When you see massive token overhead (+300%+) with no improvement
- Domains where your task uses different versions/APIs than skill examples

---

### For Skill Authors

1. **Validate against real tasks** before publishing
   - Use paired evaluation (with/without skill)
   - Measure both correctness and token overhead
   - Target ΔP > 5% to justify publication

2. **Profile token usage** during development
   - Skills causing 200%+ overhead should be redesigned
   - Aim for neutral or negative overhead (ρ ≤ 0)

3. **Test version compatibility**
   - Document framework versions skill was authored for
   - Include version selection guidance in skill text

4. **Keep skills focused and scoped**
   - Target specific problems, not broad domains
   - Compare against django-patterns (too broad) vs. gitlab-ci-patterns (focused)

5. **Prefer abstract patterns over concrete templates**
   - Use examples as illustrations, not prescriptions
   - Include version/customization guidance
   - Avoid hard-coded values that might not transfer

6. **Validate against multiple tasks**
   - Test skill on ≥10 diverse instances
   - Measure pass rates with/without skill
   - Identify failure modes before shipping

---

## Limitations & Future Work (from Paper)

### Multi-Model Evaluation
Paper evaluated only Claude Haiku 4.5. Skill utility likely modulated by:
- Model size (stronger models may find skills redundant)
- Training data composition
- Architectural differences

**Future**: Evaluate across Claude Sonnet 4.6, Opus 4.6, and open-source models

### Diverse Agent Scaffolds
Current evaluation uses Claude Code CLI. Different agent frameworks may:
- Allocate context differently
- Employ different retrieval strategies
- Structure reasoning differently

**Future**: Test across SWE-agent, OpenHands, Aider

### Dynamic Skill Selection
Current setting: One skill pre-placed per task. Real deployments require:
- Automatic skill selection from library
- Multi-skill composition
- Skill interaction effects

**Future**: Evaluate skill selection accuracy, multi-skill interference

### Skill Design Space
Current analysis: Binary success/failure. Future could explore:
- Skill granularity (atomic vs. composite)
- Abstraction levels (high-level vs. detailed)
- Structural organization (modular vs. monolithic)

---

## Conclusion

**SWE-Skills-Bench demonstrates that agent skills are a narrow intervention whose utility depends strongly on:**

1. **Domain fit**: Specialized knowledge not in base model training
2. **Abstraction level**: Focused scope matching task requirements
3. **Contextual compatibility**: Skill examples matching framework versions
4. **Concreteness**: Actual implementations vs. abstract guidance

**The benchmark refutes the "skill injection = automatic improvement" narrative.** Instead, skills are **high-risk, high-reward interventions** that require careful design, validation, and selection.

**For practitioners**: Measure before adopting. For skill authors: Validate rigorously. For platform designers: Provide tooling for paired evaluation and version management.

The future of agent skills lies not in broader skills, but in **better skill design, curation, and selection mechanisms**.

---

## Appendix: Full Results Table

| # | Skill | Category | Pass+ | Pass- | ΔP | ρ | Status |
|---|-------|----------|-------|-------|------|--------|--------|
| 1 | add-admin-api-endpoint | API Dev | 84.0% | 84.0% | 0.0% | +4.4% | ⚪ Zero |
| 2 | add-malli-schemas | API Dev | 90.0% | 90.0% | 0.0% | +49.2% | ⚪ Zero |
| 3 | add-uint-support | DevTools | 100% | 100% | 0.0% | +112.6% | ⚪ Zero |
| 4 | analytics-events | Analytics | 100% | 100% | 0.0% | +104.6% | ⚪ Zero |
| 5 | analyze-ci | Analytics | 100% | 100% | 0.0% | -10.6% | ⚪ Zero |
| 6 | bash-defensive-patterns | Security | 90.9% | 90.9% | 0.0% | +144.3% | ⚪ Zero |
| 7 | bazel-build-optimization | DevTools | 90.0% | 90.0% | 0.0% | -60.0% | ⚪ Zero |
| 8 | changelog-automation | DevTools | 70.0% | 70.0% | 0.0% | -53.3% | ⚪ Zero |
| 9 | clojure-write | DevTools | 81.8% | 81.8% | 0.0% | -33.4% | ⚪ Zero |
| 10 | creating-financial-models | DataSci | 90.0% | 90.0% | 0.0% | +0.7% | ⚪ Zero |
| 11 | dbt-transformation-patterns | DataSci | 100% | 100% | 0.0% | +103.2% | ⚪ Zero |
| 12 | django-patterns | API Dev | 81.8% | 90.9% | **-9.1%** | +4.2% | 🔴 Neg |
| 13 | distributed-tracing | Analytics | 100% | 92.3% | **+7.7%** | -30.4% | 🟢 Pos |
| 14 | fix | DevTools | 91.7% | 91.7% | 0.0% | +153.0% | ⚪ Zero |
| 15 | github-actions-templates | DevOps | 70.0% | 70.0% | 0.0% | +39.1% | ⚪ Zero |
| 16 | gitops-workflow | DevOps | 100% | 100% | 0.0% | +127.1% | ⚪ Zero |
| 17 | gitlab-ci-patterns | DevOps | 78.6% | 64.3% | **+14.3%** | +58.6% | 🟢 Pos |
| 18 | grafana-dashboards | Analytics | 100% | 100% | 0.0% | +29.3% | ⚪ Zero |
| 19 | implementing-agent-modes | DevTools | 100% | 100% | 0.0% | -47.8% | ⚪ Zero |
| 20 | implementing-jsc-classes-zig | DevTools | 90.0% | 90.0% | 0.0% | +22.0% | ⚪ Zero |
| 21 | istio-traffic-management | DevOps | 100% | 92.9% | **+7.1%** | -22.0% | 🟢 Pos |
| 22 | k8s-manifest-generator | DevOps | 100% | 100% | 0.0% | +91.2% | ⚪ Zero |
| 23 | langsmith-fetch | DevTools | 100% | 100% | 0.0% | +5.9% | ⚪ Zero |
| 24 | linkerd-patterns | DevOps | 90.9% | 100.0% | **-9.1%** | +50.3% | 🔴 Neg |
| 25 | llm-evaluation | DataSci | 100% | 100% | 0.0% | +17.6% | ⚪ Zero |
| 26 | mcp-builder | DevTools | 100% | 100% | 0.0% | +36.1% | ⚪ Zero |
| 27 | nx-workspace-patterns | DevTools | 100% | 100% | 0.0% | +14.5% | ⚪ Zero |
| 28 | prometheus-configuration | Analytics | 100% | 100% | 0.0% | -27.8% | ⚪ Zero |
| 29 | prompt-engineering-patterns | LLM | 100% | 90.0% | **+10.0%** | +46.4% | 🟢 Pos |
| 30 | python-anti-patterns | DevTools | 100% | 100% | 0.0% | -44.1% | ⚪ Zero |
| 31 | python-background-jobs | DataSci | 100% | 100% | 0.0% | +236.8% | ⚪ Zero |
| 32 | python-configuration | DataSci | 91.7% | 91.7% | 0.0% | +29.7% | ⚪ Zero |
| 33 | python-observability | Analytics | 100% | 100% | 0.0% | +157.5% | ⚪ Zero |
| 34 | python-packaging | DevTools | 100% | 100% | 0.0% | +123.9% | ⚪ Zero |
| 35 | python-performance-optimization | DevTools | 100% | 100% | 0.0% | -5.1% | ⚪ Zero |
| 36 | python-resilience | DevOps | 100% | 100% | 0.0% | -77.6% | ⚪ Zero |
| 37 | rag-implementation | DataSci | 100% | 100% | 0.0% | +44.5% | ⚪ Zero |
| 38 | **risk-metrics-calculation** | **DataSci** | **100%** | **70%** | **+30.0%** | **-34.8%** | **🟢 Pos** ⭐⭐ |
| 39 | security-review | Security | 92.3% | 92.3% | 0.0% | +0.9% | ⚪ Zero |
| 40 | service-mesh-observability | Analytics | 100% | 100% | 0.0% | +450.8% | ⚪ Zero |
| 41 | similarity-search-patterns | DataSci | 100% | 90.0% | **+10.0%** | -32.4% | 🟢 Pos |
| 42 | slo-implementation | Analytics | 100% | 100% | 0.0% | -40.2% | ⚪ Zero |
| 43 | spark-optimization | DataSci | 100% | 100% | 0.0% | +23.9% | ⚪ Zero |
| 44 | springboot-tdd | Security | 70.0% | 80.0% | **-10.0%** | -36.8% | 🔴 Neg |
| 45 | tdd-workflow | Security | 28.6% | 21.4% | **+7.1%** | +78.6% | 🟢 Pos |
| 46 | turborepo | DevTools | 50.0% | 50.0% | 0.0% | +187.9% | ⚪ Zero |
| 47 | v3-performance-optimization | DevTools | 100% | 100% | 0.0% | -56.4% | ⚪ Zero |
| 48 | vector-index-tuning | DataSci | 90.0% | 90.0% | 0.0% | +18.8% | ⚪ Zero |
| 49 | xlsx | Analytics | 36.4% | 36.4% | 0.0% | -18.1% | ⚪ Zero |

**Summary Statistics**:
- 🟢 **Positive (7)**: +7.1% to +30.0% improvements
- ⚪ **Neutral (39)**: 0.0% improvement
- 🔴 **Negative (3)**: -9.1% to -10.0% degradation

---

**Report Generated**: March 24, 2026
**Source**: SWE-Skills-Bench (arXiv:2603.15401v1)
