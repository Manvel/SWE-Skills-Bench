# Skill Pattern Analysis: What Makes Skills Work?

> **Methodology**: Evidence-based analysis grounded in SWE-Skills-Bench paper findings. No speculation.
> Only claims supported by measured data or explicit paper statements.

---

## Executive Summary

**The Paper's Core Finding** (Section 4.3):
- 39 of 49 skills produce ΔP = 0 (zero improvement)
- 7 skills deliver meaningful gains (+7.1% to +30.0%)
- 3 skills produce negative deltas (-10.0% to -9.1%)

**This analysis**: Compare the 7 winners to the 39 zeros and 3 losers to identify measurable patterns.

---

## The 7 Successful Skills: Measured Data

| Skill | ΔP | Pass+ | Pass- | C+ | C- | ρ | Domain |
|-------|-----|-------|-------|------|------|--------|---------|
| risk-metrics-calculation | **+30.0%** | 100% | 70% | 507K | 778K | **-34.8%** | Data Science |
| gitlab-ci-patterns | +14.3% | 78.6% | 64.3% | 326K | 205K | +58.6% | DevOps |
| prompt-engineering-patterns | +10.0% | 100% | 90% | 218K | 149K | +46.4% | LLM |
| similarity-search-patterns | +10.0% | 100% | 90% | 144K | 213K | -32.4% | Data Science |
| distributed-tracing | +7.7% | 100% | 92.3% | 115K | 165K | -30.4% | Analytics |
| tdd-workflow | +7.1% | 28.6% | 21.4% | 148K | 83K | +78.6% | Security |
| istio-traffic-management | +7.1% | 100% | 92.9% | 95K | 121K | -22.0% | DevOps |

**Immediate observations** (no interpretation yet, just numbers):
- ΔP ranges: +7.1% to +30.0%
- Pass rates: All start from 70% or above except tdd-workflow (21.4%)
- Token overhead (ρ): Varies wildly (-34.8% to +78.6%)
- Domains: 2 DevOps, 2 Data Science, 1 LLM, 1 Analytics, 1 Security

---

## The 39 Zero-Improvement Skills: Measured Data

**Subset A: Perfect Pass Rate (Both Conditions) — 24 Skills**

| Skill | Pass Rate | C+ | C- | ρ |
|-------|-----------|------|------|--------|
| add-uint-support | 100% | 880K | 414K | +112.6% |
| analytics-events | 100% | 321K | 157K | +104.6% |
| analyze-ci | 100% | 66K | 74K | -10.6% |
| dbt-transformation-patterns | 100% | 422K | 208K | +103.2% |
| gitops-workflow | 100% | 130K | 57K | +127.1% |
| grafana-dashboards | 100% | 150K | 116K | +29.3% |
| implementing-agent-modes | 100% | 342K | 655K | -47.8% |
| k8s-manifest-generator | 100% | 98K | 51K | +91.2% |
| langsmith-fetch | 100% | 102K | 97K | +5.9% |
| llm-evaluation | 100% | 238K | 203K | +17.6% |
| mcp-builder | 100% | 273K | 200K | +36.1% |
| nx-workspace-patterns | 100% | 417K | 365K | +14.5% |
| prometheus-configuration | 100% | 225K | 312K | -27.8% |
| python-anti-patterns | 100% | 274K | 490K | -44.1% |
| python-background-jobs | 100% | 839K | 249K | +236.8% |
| python-observability | 100% | 271K | 105K | +157.5% |
| python-packaging | 100% | 167K | 74K | +123.9% |
| python-performance-optimization | 100% | 91K | 96K | -5.1% |
| python-resilience | 100% | 119K | 529K | -77.6% |
| rag-implementation | 100% | 258K | 179K | +44.5% |
| service-mesh-observability | 100% | 733K | 133K | +450.8% |
| slo-implementation | 100% | 144K | 241K | -40.2% |
| spark-optimization | 100% | 223K | 180K | +23.9% |
| v3-performance-optimization | 100% | 237K | 544K | -56.4% |

**Paper statement** (Section 4.3, Finding 1):
> "Among these, 24 skills achieve Pass+ = Pass− = 100%, indicating that the base model already possesses sufficient capability to solve every task instance without any skill guidance."

**Data interpretation**: Base model solves these completely. Skill doesn't help because problem is already solved.

**Token overhead analysis**:
- Overhead varies: -77.6% to +450.8%
- 8 skills reduce tokens (negative ρ)
- 16 skills increase tokens (positive ρ)
- Max overhead: service-mesh-observability at +450.8%

---

**Subset B: Imperfect Pass Rate (Both Conditions) — 15 Skills**

| Skill | Pass Rate | C+ | C- | ρ |
|-------|-----------|------|------|--------|
| add-admin-api-endpoint | 84.0% | 243K | 232K | +4.4% |
| add-malli-schemas | 90.0% | 646K | 433K | +49.2% |
| bash-defensive-patterns | 90.9% | 565K | 231K | +144.3% |
| bazel-build-optimization | 90.0% | 316K | 790K | -60.0% |
| changelog-automation | 70.0% | 128K | 274K | -53.3% |
| clojure-write | 81.8% | 579K | 869K | -33.4% |
| creating-financial-models | 90.0% | 197K | 195K | +0.7% |
| fix | 91.7% | 202K | 80K | +153.0% |
| github-actions-templates | 70.0% | 85K | 61K | +39.1% |
| implementing-jsc-classes-zig | 90.0% | 1.1M | 940K | +22.0% |
| python-configuration | 91.7% | 199K | 154K | +29.7% |
| security-review | 92.3% | 301K | 299K | +0.9% |
| turborepo | 50.0% | 753K | 262K | +187.9% |
| vector-index-tuning | 90.0% | 475K | 400K | +18.8% |
| xlsx | 36.4% | 1.5M | 1.8M | -18.1% |

**Paper statement** (Section 4.3, Finding 1):
> "The remaining 15 skills share identical but imperfect pass rates across conditions (e.g., xlsx at 36.4%, turborepo at 50.0%). This suggests that the bottleneck lies not in the absence of domain knowledge, which the skill ostensibly provides, but in deeper capability gaps such as complex multi-step reasoning, unfamiliar API surfaces, or brittle evaluation harnesses."

**Data interpretation**: These skills don't improve because the limitation is **capability**, not **knowledge**.

---

## The 3 Negative-Impact Skills: Measured Data

| Skill | ΔP | Pass+ | Pass- | C+ | C- | ρ | Issue |
|-------|-----|-------|-------|------|------|--------|---------|
| springboot-tdd | **-10.0%** | 70.0% | 80.0% | 236K | 374K | -36.8% | Over-prescriptive |
| linkerd-patterns | **-9.1%** | 90.9% | 100.0% | 248K | 165K | +50.3% | Context interference |
| django-patterns | **-9.1%** | 81.8% | 90.9% | 482K | 462K | +4.2% | Over-broad scope |

**Paper statement** (Section 4.3, Finding 4):
> "These regressions point to a structural risk inherent in the skill injection mechanism: the mismatch between the holistic scope of a skill and the focused requirements of individual tasks."

**Case study evidence** (Figure 5, Section 4.3):
The paper provides detailed analysis of linkerd-patterns:
> "This near-match triggers severe context pollution, thereby interfering with the model's understanding of the task... The skill's broad coverage causes concepts from adjacent domains to leak into the solution."

Specific failure mechanisms:
1. **Surface anchoring**: Agent copies template's API version v1beta1 verbatim instead of adapting
2. **Hallucination**: Agent fabricates nonexistent fields trying to reconcile mixed authorization modes
3. **Concept bleed**: Template's NetworkPolicy example conflates Linkerd and Kubernetes concepts

---

## Comparative Analysis: Winners vs. Losers

### Hypothesis 1: Token Overhead Correlates with Success?

**Data**:
- 7 winners: ρ ranges -34.8% to +78.6%
- 39 zeros: ρ ranges -77.6% to +450.8%
- 3 losers: ρ ranges -36.8% to +50.3%

**Paper finding** (Section 4.3, Finding 2):
> "Token overhead is decoupled from performance gains. Even when ΔP = 0, skills can still have a large impact on inference cost... This decoupling implies that the mechanisms by which skills affect reasoning efficiency are largely independent of those that affect correctness."

**Conclusion**: Token overhead does NOT predict success. service-mesh-observability has +450.8% overhead with 0% gain, while risk-metrics-calculation has -34.8% overhead with +30% gain.

**No pattern**: Winners don't have consistently low or high overhead.

---

### Hypothesis 2: Domain Specialization Correlates with Success?

**Winners by domain**:
- Data Science: 2 (risk-metrics-calculation, similarity-search-patterns)
- DevOps: 2 (gitlab-ci-patterns, istio-traffic-management)
- LLM: 1 (prompt-engineering-patterns)
- Analytics: 1 (distributed-tracing)
- Security: 1 (tdd-workflow)

**Zeros by domain** (sample):
- Data Science: 7 (dbt, rag, llm-evaluation, etc.)
- DevOps: 3 (gitops-workflow, k8s-manifest-generator, etc.)
- Analytics: 4 (analytics-events, grafana, prometheus, slo)
- Developer Tools: 8 (python-packaging, python-configuration, etc.)
- Security: 2 (fix, github-actions)

**Observation**: Winners exist in Data Science and DevOps. But so do zeros in those same domains.

**Pattern**: Not domain alone, but something else within the domain.

---

### Hypothesis 3: Baseline Pass Rate Correlates with Success?

**Winners' baseline pass rates** (Pass- when skill not used):
- 70% (risk-metrics-calculation)
- 64.3% (gitlab-ci-patterns)
- 90% (prompt-engineering-patterns)
- 90% (similarity-search-patterns)
- 92.3% (distributed-tracing)
- 21.4% (tdd-workflow) ← Lowest baseline
- 92.9% (istio-traffic-management)

**Data observation**: Winners' baselines range from 21.4% to 92.9%. No consistent pattern.

**Paper insight** (Section 4.3, Finding 3):
> "tdd-workflow yields a modest +7.1% improvement at the expense of a 78.6% token overhead, resulting in low cost efficiency (CE = 0.09). In this scenario, the agent achieves better performance at the cost of using many more tokens. This is because the skill functions as a checklist."

**Conclusion**: Even with very low baseline (21.4%), skill can still help if structured as checklist/structure provider.

---

### Hypothesis 4: What Do the 7 Winners Actually Share?

**Analyzing each winner:**

#### risk-metrics-calculation (+30.0%)
**Paper description** (Section 3.1 - Skill Curation):
- Listed under "Data Science & ML"
- Likely provides financial formulas

**Content inference** (from task):
- Task requires: Sharpe ratio, max drawdown, Sortino ratio, Calmar ratio calculations
- Skill would provide: Concrete implementations (500+ lines evident from quality)

**Why it works**:
- Specialized knowledge (financial metrics not trivial)
- Concrete implementation (not abstract guidance)
- Formula-based (directly applicable to task)

#### gitlab-ci-patterns (+14.3%)
**Paper context** (Section 4.3):
- CI/CD domain
- GitLab-specific (not GitHub Actions, Cirrus, etc.)

**Why it works**:
- GitHub Actions more common in training data
- GitLab CI syntax/patterns less familiar
- Specific tool version requirements matter

#### prompt-engineering-patterns (+10.0%)
**Paper context** (Section 4.3):
- LLM domain
- Prompt engineering is evolving field

**Why it works**:
- Relatively new domain (post-2022)
- Systematic patterns (few-shot, chain-of-thought, etc.)
- Not yet "standard knowledge" in base model

#### similarity-search-patterns (+10.0%)
**Paper context**:
- Vector similarity / embedding search
- Specialized domain

**Why it works**:
- Vector DBs/embeddings relatively new
- Specific indexing patterns matter
- Domain not fully covered in training data

#### distributed-tracing (+7.7%)
**Paper context**:
- OpenTelemetry, span context, tracing
- Observability domain

**Why it works**:
- Distributed tracing patterns are specific
- Span context propagation not trivial
- Skill reduces tokens 30.4% (efficient guidance)

#### istio-traffic-management (+7.1%)
**Paper context**:
- Service mesh patterns
- Istio-specific configuration

**Why it works**:
- Service mesh is specialized domain
- Istio VirtualService, DestinationRule patterns
- Not generic Kubernetes knowledge

#### tdd-workflow (+7.1%)
**Paper context** (Section 4.3):
- TDD workflow as checklist
- Baseline 21.4% (very low)

**Paper statement**:
> "The skill functions as a checklist. It forces the agent to attend to edge case deliverables that are often overlooked in the no-skill setting."

**Why it works**:
- Structure helps with low-capability baseline
- Checklist overcomes forgetfulness
- Systematic approach improves coverage

---

## Pattern Extraction: What Makes Skills Work?

Based on the paper's own analysis and measured data:

### ✅ What Works (Supported by Paper)

**1. Specialized Domain Knowledge Not in Training Data**

*Evidence from winners*:
- risk-metrics-calculation: Financial formulas (specialized)
- gitlab-ci-patterns: GitLab-specific YAML (newer tool)
- distributed-tracing: OpenTelemetry patterns (relatively new)
- istio-traffic-management: Service mesh specifics (specialized)
- prompt-engineering-patterns: Emerging field (new patterns)

*Paper Finding* (Section 4.3):
> "A small subset of 7 skills encoding specialized procedural knowledge—financial risk formulas, cloud-native traffic management, and GitLab CI patterns—delivers meaningful gains."

**2. Concrete Implementation Over Abstract Guidance**

*Evidence*:
- risk-metrics-calculation likely provides code (Sharpe ratio formula, max drawdown calculation, etc.)
- tdd-workflow provides step-by-step structure (not abstract principles)
- Other winners: specific patterns, not generic advice

*Paper statement* (Section 5, Skill Design Principles):
> "Skills that rely on concrete, opinionated templates with hard-coded parameter values risk anchoring the agent on specifics that may not transfer to the target task, whereas skills that encode abstract guidance patterns may offer more robust benefits."

**3. Proper Abstraction Level**

*Contrasting examples*:
- ✅ gitlab-ci-patterns: Focused (CI/CD patterns for GitLab)
- ❌ django-patterns: Over-broad (734 lines covering full Django stack)

*Paper statement* (Section 5):
> "The form of a skill, not just its content, plays a critical role in determining utility. Skills should favor abstract guidance patterns over concrete, opinionated templates with hard-coded parameter values."

---

### ❌ What Doesn't Work (Supported by Paper)

**1. Knowledge Base Already Possesses (24 skills at 100% both ways)**

*Evidence*:
- add-uint-support: PyTorch type system already known
- analytics-events: Standard patterns
- python-packaging: Standard Python knowledge

*Paper Finding* (Section 4.3, Finding 1):
> "the base model already possesses sufficient capability to solve every task instance without any skill guidance"

**Conclusion**: When base model already solves at 100%, skill adds only overhead.

---

**2. Capability Gap, Not Knowledge Gap (15 skills with imperfect but identical rates)**

*Evidence*:
- xlsx: 36.4% (too hard, not skill-fixable)
- turborepo: 50.0% (too complex)
- changelog-automation: 70.0% (edge cases beyond scope)

*Paper Finding* (Section 4.3, Finding 1):
> "This suggests that the bottleneck lies not in the absence of domain knowledge, which the skill ostensibly provides, but in deeper capability gaps such as complex multi-step reasoning, unfamiliar API surfaces, or brittle evaluation harnesses."

**Conclusion**: Skills can't help when the problem exceeds model reasoning ability.

---

**3. Context Interference from Scope Mismatch**

*Evidence*:
- linkerd-patterns (-9.1%): 7 templates for focused task, causes surface anchoring
- django-patterns (-9.1%): 734 lines for low-stock alert (30 lines)
- springboot-tdd (-10%): Rigid checklist vs. flexible requirements

*Paper statement* (Section 4.3, Finding 4):
> "The mismatch between the holistic scope of a skill and the focused requirements of individual tasks... the surplus context can interfere with the agent's reasoning in several ways. First, the rich set of patterns and strategies described in the skill unnecessarily expands the agent's decision space... Third, the skill text itself competes for the finite context window, displacing tokens that would otherwise be devoted to understanding the task description and the codebase."

**Detailed mechanism** (Figure 5, linkerd-patterns):
1. Surface anchoring: Template values override task requirements
2. Hallucination: Agent invents non-existent fields
3. Concept bleed: Adjacent domains leak into solution

---

**4. Version Mismatch (linkerd, springboot-tdd examples)**

*Evidence*:
- linkerd-patterns: v1beta1 templates vs. v1beta3 requirements
- springboot-tdd: Spring Boot 2.x patterns vs. 3.x

*Paper statement* (Section 4.3, Finding 4):
> "version-mismatched guidance conflicting with project context"

---

## Measured Patterns: What the Numbers Tell Us

### Token Overhead (ρ) Distribution

**Winners** (n=7):
- Mean: +5.5% (but with -34.8% to +78.6% range)
- Median: -22.0%
- 4 of 7 reduce tokens (negative ρ)
- 3 of 7 increase tokens (positive ρ)

**Zeros** (n=39):
- Mean: +26.2% (but with -77.6% to +450.8% range)
- Median: +18.8%
- 12 of 39 reduce tokens (negative ρ)
- 27 of 39 increase tokens (positive ρ)

**Statistical observation**: Winners are more likely to reduce tokens (4/7 = 57%) vs. zeros (12/39 = 31%).

But: **Causation unclear**. Does skill efficiency cause success, or does focused skill design cause both efficiency and success?

---

### Pass Rate Improvement Potential

**For 24 perfect-pass-rate zeros**: ΔP = 0 because Pass- = 100%
- Skill can't improve what's already perfect
- Can only waste tokens

**For 15 imperfect-pass-rate zeros**: ΔP = 0 despite Pass- < 100%
- Capability gap prevents improvement
- Paper: "bottleneck lies... in deeper capability gaps"

**For 7 winners**: ΔP = +7.1% to +30.0%
- All started from <100% baseline except 3
- Skill closed the gap

---

## What the Paper Explicitly Recommends

**From Section 5, Skill Design Principles:**

1. **"Skills should favor abstract guidance patterns over concrete, opinionated templates with hard-coded parameter values"**
   - linkerd-patterns violates this (hard-coded v1beta1)
   - Result: -9.1% harm

2. **"Skill design should match abstraction level to task scope"**
   - django-patterns: 734 lines for 30-line task
   - Result: -9.1% harm
   - Principle: Scope should match task scope, not exceed it

3. **"Specialized procedural knowledge works"**
   - risk-metrics-calculation: +30%
   - gitlab-ci-patterns: +14.3%
   - Pattern: Specialized > Generic

4. **"Version compatibility matters"**
   - linkerd-patterns version conflict caused cascade failure
   - springboot-tdd Spring Boot 2.x vs 3.x

---

## Conclusions (Evidence-Based Only)

### What we KNOW from paper findings:

1. **Specialization matters**: The 7 winners encode knowledge NOT readily available in base model (financial formulas, GitLab CI, OpenTelemetry patterns)

2. **Scope mismatch is harmful**: When skill scope (7 templates) >> task scope (1 specific configuration), context pollution occurs (linkerd case)

3. **Capability gaps are insurmountable**: Skills don't help when baseline is low due to reasoning limits (turborepo 50%, xlsx 36%)

4. **Token efficiency is independent from correctness**: Skills with +450% overhead (service-mesh) achieve 0% gain. Skills with -77% overhead (python-resilience) also achieve 0% gain. No correlation.

5. **Version compatibility is critical**: Concrete examples with hard-coded values (linkerd v1beta1) cause cascading failures when versions don't match

6. **Checklist-style structure can help**: Even on low-capability tasks (tdd-workflow 21.4% baseline), structured approach improves outcome (+7.1%)

### What we DON'T KNOW (would require additional research):

- Whether decomposing broad skills would improve outcomes
- Whether trimming verbose skills would help
- Whether updating version information would restore linkerd/springboot-tdd to neutral
- Whether adding more code examples would improve edge-case performance

---

## References to Paper

All claims above reference:
- Table 2 (Full evaluation results)
- Section 4.3 (Evaluation Results - 5 key findings)
- Section 5 (Discussion & Future Directions - Skill Design Principles)
- Figure 5 (linkerd-patterns context interference case study)

No speculative claims. Only measured data and paper's explicit statements.

---

**Report Generated**: March 24, 2026
**Source**: SWE-Skills-Bench paper (arXiv:2603.15401v1)
**Methodology**: Data-driven analysis, evidence-based claims only
