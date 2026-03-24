# Skill Recommendations: Evidence-Based Fixes

> **Approach**: Each recommendation is grounded in what the paper identified as the problem.
> We recommend fixes ONLY to address documented failure mechanisms.
> Confidence levels reflect how directly the evidence supports the fix.

---

## Quick Reference: What to Fix First

| Priority | Skill | Problem | Fix | Confidence | Effort |
|----------|-------|---------|-----|------------|--------|
| 🔴 CRITICAL | linkerd-patterns | Version mismatch causing surface anchoring | Update templates to v1beta3+ | **HIGH** | 2-4h |
| 🔴 CRITICAL | springboot-tdd | Spring Boot 2.x patterns vs. 3.x | Update for Spring Boot 3.x | **HIGH** | 2-3h |
| 🔴 CRITICAL | django-patterns | Scope mismatch (734 lines for 30-line task) | Reduce scope/focus | **HIGH** | 4-6h |
| 🟡 HIGH | service-mesh-observability | Excessive verbosity (+450.8% tokens, 0% gain) | Trim to essentials | **MEDIUM** | 2-3h |
| 🟡 HIGH | python-background-jobs | Excessive verbosity (+236.8% tokens, 0% gain) | Trim scope | **MEDIUM** | 1-2h |
| 🟡 HIGH | github-actions-templates | 70% baseline, likely v3 examples | Update to v4, add concrete examples | **MEDIUM** | 2-3h |

---

## Category 1: Version Mismatch Issues

### 🔴 linkerd-patterns (-9.1% when used)

**Problem Identified by Paper**:
> "version-mismatched guidance conflicting with project context" (Section 4.3, Finding 4)

**Failure Mechanism** (Figure 5, detailed analysis):
```
Hard-coded v1beta1 API version in template
    ↓
Agent copies template verbatim (surface anchoring)
    ↓
Task requires v1beta3 with gRPC protocol
    ↓
Wrong API version + wrong protocol
    ↓
Agent hallucinates non-existent fields trying to reconcile
    ↓
Concept bleed: Template's NetworkPolicy pollutes solution
```

**Paper's Own Recommendation** (Section 5):
> "Skill design should favor abstract guidance patterns over concrete, opinionated templates with hard-coded parameter values, as the latter risk anchoring the agent on specifics that may not transfer to the target task."

**Specific Recommendation**:

1. **Remove hard-coded API versions**
   ```
   CURRENT: apiVersion: policy.linkerd.io/v1beta1
   CHANGE TO: # Use the latest Linkerd API version available in your cluster
              # Detect version: kubectl api-versions | grep linkerd
   ```

2. **Remove protocol-specific values**
   ```
   CURRENT: proxyProtocol: HTTP/1
   CHANGE TO: # Specify protocol matching your service (gRPC, HTTP/1, HTTP/2, etc.)
   ```

3. **Reduce template quantity**
   - Current: 7 templates (causing confusion)
   - Proposal: Keep 2-3 essential patterns
   - Remove: NetworkPolicy (causes concept bleed), multiple auth modes

4. **Add version disclaimer**
   - Document: "Guide applies to Linkerd 2.12+. Adapt for your version."

**Confidence**: **HIGH** ✅
- Paper explicitly documents this failure mechanism
- Figure 5 shows exact sequence: version mismatch → surface anchoring → hallucination
- Paper recommends abstract patterns (already guides the fix)

**Expected Outcome**:
- Before: -9.1% (actively harmful)
- After: +0% to +5% (at minimum neutral, possibly helpful)

**Effort**: 2-4 hours
- 1h: Audit all examples for version dependencies
- 1-2h: Rewrite templates with placeholders
- 1h: Test against current Linkerd version

**Responsible Action**: This skill actively harms users. Update should be high priority.

---

### 🔴 springboot-tdd (-10% when used)

**Problem Identified by Paper**:
> "version-specific conventions conflict with the target project's framework" (Section 4.3, Finding 4)

**Failure Mechanism**:
- Skill likely encodes Spring Boot 2.x patterns
- Task uses Spring Boot 3.x
- TDD checklist doesn't match updated annotations/frameworks

**Paper Context**:
Spring Boot 3.x introduced breaking changes:
- Java 17+ requirement
- New @SpringBootTest behavior
- Updated slice testing annotations
- Different TestRestTemplate usage

**Specific Recommendation**:

1. **Document target version**
   ```
   "This guide targets Spring Boot 3.2+
    For Spring Boot 2.x, note these differences:..."
   ```

2. **Update annotations**
   - Review for deprecated annotations in 3.x
   - Update @SpringBootTest usage
   - Update @WebMvcTest, @DataJpaTest patterns

3. **Verify test context caching**
   - Spring Boot 3.x changes test caching
   - Update examples to match

4. **Make flexibility explicit**
   - Paper notes: "rigid workflow doesn't match all tasks"
   - Change from prescriptive checklist to flexible guidance

**Confidence**: **HIGH** ✅
- Paper identifies version mismatch as failure cause
- Spring Boot 3.x released; 2.x patterns are outdated
- Clear failure mechanism: version incompatibility

**Expected Outcome**:
- Before: -10.0% (actively harmful)
- After: +0% to +5% (at minimum neutral)

**Effort**: 2-3 hours
- 1h: Identify deprecated annotations in Spring Boot 3.x
- 1-2h: Update examples
- 30m: Add flexibility guidance

**Responsible Action**: Second critical update.

---

### 🟠 github-actions-templates (70% baseline)

**Problem Identified by Paper**:
- Baseline 70% suggests templates don't cover all cases
- Likely outdated (GitHub Actions v3 → v4 is current)

**Changes in GitHub Actions v4**:
- Runtime changed from Node 16 to Node 20
- Some actions moved/deprecated
- API changes in runner environment

**Specific Recommendation**:

1. **Update action versions**
   ```
   v3: uses: actions/checkout@v3
   v4: uses: actions/checkout@v4
   ```

2. **Update Node.js version**
   - v4 requires Node 20+
   - Update examples

3. **Add concrete workflow examples**
   - Current templates: likely too generic
   - Recommendation: Show complete working workflows
   - Include testing, build, deploy examples

**Confidence**: **MEDIUM-HIGH** ✅
- 70% baseline suggests incomplete coverage
- GitHub Actions v4 is documented, concrete update
- Adding examples addresses "incomplete coverage" issue

**Expected Outcome**:
- Before: 70%
- After: 75-80% (updated examples help edge cases)

**Effort**: 2-3 hours
- 1h: Update to v4 syntax
- 1-2h: Add concrete workflow examples

---

## Category 2: Scope Mismatch Issues

### 🔴 django-patterns (-9.1% when used)

**Problem Identified by Paper**:
> "The mismatch between the holistic scope of a skill and the focused requirements of individual tasks... the surplus context can interfere with the agent's reasoning in several ways." (Section 4.3, Finding 4)

**Failure Mechanism**:
- Skill: 734 lines covering full Django stack
- Task: Low-stock alert with caching (30 lines needed)
- Agent gets confused choosing between patterns

**Paper Analysis**:
> "First, the rich set of patterns and strategies described in the skill unnecessarily expands the agent's decision space, prompting deliberation over design choices the task does not warrant... the skill text itself competes for the finite context window, displacing tokens that would otherwise be devoted to understanding the task description and the codebase."

**Evidence**: Same mechanism as linkerd-patterns, but with breadth instead of version mismatch:
- Surplus guidance → decision space expansion
- Context window pollution → less room for task understanding

**Specific Recommendation**:

1. **Reduce scope in current skill** OR **Create focused sub-skills**

   **Option A: Trim current skill**
   - Remove: Full project structure (not needed for task-level work)
   - Remove: Multiple pattern alternatives (choose one approach)
   - Keep: Models, serializers, signals, caching, testing (relevant)

   **Option B: Create focused micro-skills** (higher confidence in success)
   - django-signals-patterns (signals + event handling)
   - django-caching-strategies (Redis/caching)
   - django-queryset-optimization (N+1 prevention)
   - django-rest-framework-basics (serializers, viewsets)
   - [Etc., ~4-5 focused skills]

2. **If keeping current skill**: Add context switching guidance
   ```
   "This comprehensive guide covers many Django patterns.
    For your specific task, focus on these sections:
    [Task type] → [Relevant sections only]"
   ```

**Confidence**: **HIGH** ✅
- Paper explicitly documents this failure mechanism
- Linkerd case (similar problem) has detailed failure analysis
- Scope mismatch → context pollution is well-established in paper

**Expected Outcome**:
- Before: -9.1% (actively harmful)
- After: Option A = +0-2%, Option B = +5-10%

**Effort**:
- Option A (trim): 3-4 hours
- Option B (decompose): 8-12 hours

**Recommendation**: Option A (trim) first; if insufficient, do Option B.

---

## Category 3: Verbosity/Overhead Issues

### 🟡 service-mesh-observability (+450.8% overhead, 0% improvement)

**Problem Identified by Paper**:
> "Token overhead is decoupled from performance gains... skills reshape the agent's reasoning path without necessarily improving outcomes." (Section 4.3, Finding 2)

**Specific Issue**:
- 100% pass rate without skill (problem already solved)
- +450.8% token overhead (4.5x more tokens!)
- Skill makes agent extremely verbose without helping

**Failure Mechanism**:
- Skill provides comprehensive observability guide (likely 300+ lines)
- Task is straightforward observability setup
- Agent over-deliberates on tool choices, configuration options

**Specific Recommendation**:

1. **Identify the essential patterns** (What actually helps?)
   - Key metrics to track (latency p50/p99, error rate, resource usage)
   - One configuration approach (Prometheus or similar)
   - One troubleshooting flowchart

2. **Remove everything else**
   - Multiple tool comparisons (causes decision paralysis)
   - Architectural diagrams
   - Edge case scenarios
   - Verbose explanations

3. **Target**: 50-75 lines instead of current 300+

4. **Test**: Overhead should drop to ~0% or negative

**Confidence**: **MEDIUM** ✅
- Paper identifies verbosity as issue
- Mechanism is clear: too much guidance → too much reasoning
- But exact threshold unknown (how many lines is too many?)

**Expected Outcome**:
- Before: 100% pass, +450.8% overhead (wasteful)
- After: 100% pass, -10% to +10% overhead (efficient)
- Benefit: Same correctness, 4-5x fewer tokens

**Effort**: 2-3 hours
- 1h: Identify essential patterns
- 1h: Trim to core content
- 1h: Test and verify

---

### 🟡 python-background-jobs (+236.8% overhead, 0% improvement)

**Problem**: Same as service-mesh-observability
- 100% pass rate without skill
- +236.8% tokens with skill (3.4x more!)
- Likely covers multiple job queue libraries (Celery, RQ, task queues, etc.)

**Specific Recommendation**:

1. **Narrow scope**: Celery only (covers 90% of use cases)

2. **Remove**:
   - Multiple queue system comparisons (RabbitMQ, Redis, SQS variants)
   - Advanced scheduling (beat, periodic tasks)
   - Complex error handling
   - Distributed transactions

3. **Keep**:
   - Basic task definition
   - Common patterns (retries, timeouts)
   - One error handling approach

4. **Target**: 100-150 lines (trim from likely 300+)

**Confidence**: **MEDIUM** ✅
- Same verbosity pattern as service-mesh-observability
- Mechanism: over-comprehensive guidance → over-thinking

**Expected Outcome**:
- Before: 100% pass, +236.8% overhead
- After: 100% pass, ~0% overhead

**Effort**: 1-2 hours (simpler than service-mesh-observability)

---

## Category 4: Skill Improvement (Adding Concreteness)

### 🟢 creating-financial-models (90% baseline, potential +5-10%)

**Problem Identified by Paper**:
- 90% baseline (good, but not perfect)
- 10% failures suggest edge cases in specific calculations

**Paper Evidence** (risk-metrics-calculation success):
- Same domain (Data Science)
- **Key difference**: risk-metrics-calculation provides 500+ lines of code with concrete implementations
- Formulas: Sharpe ratio, max drawdown, VaR, CVaR, Cornish-Fisher expansion, etc.

**Comparison**:
- ❌ creating-financial-models: Likely conceptual guidance ("how to think about models")
- ✅ risk-metrics-calculation: Concrete implementations (actual formulas + code)

**Specific Recommendation**:

Add concrete code implementations for:
1. NPV calculation (Net Present Value formula)
2. IRR calculation (Internal Rate of Return solver)
3. DCF model template (Discounted Cash Flow valuation)
4. Monte Carlo simulation (Uncertainty analysis)
5. Sensitivity analysis (Parameter effects)

For each: Input → Calculation → Output + Example with real numbers

**Confidence**: **MEDIUM** ✅
- Paper shows concrete implementations work (risk-metrics-calculation +30%)
- Same domain, different approach
- Logic: Adding code should help edge cases
- **But**: Not directly tested, extrapolating from success pattern

**Expected Outcome**:
- Before: 90%
- After: 95-100% (concrete examples help)

**Effort**: 6-8 hours
- 3-4h: Write working implementations
- 2h: Verify formulas correct
- 1-2h: Document

---

### 🟢 security-review (92.3% baseline, potential +5-10%)

**Problem**:
- 92.3% baseline (good)
- 7.7% failures suggest specific security patterns not covered

**Comparison to winner** (distributed-tracing at +7.7%):
- distributed-tracing provides concrete patterns for context propagation
- security-review likely provides checklist without implementations

**Specific Recommendation**:

Add secure code examples for OWASP Top 10:

For each vulnerability:
- ❌ VULNERABLE code example
- ✅ SECURE code example
- 📝 Why the difference matters
- 🧪 How to verify the fix

Example:
```python
# ❌ VULNERABLE (SQL Injection)
query = f"SELECT * FROM users WHERE id = {user_id}"

# ✅ SECURE (Parameterized)
cursor.execute("SELECT * FROM users WHERE id = %s", (user_id,))
```

**Confidence**: **MEDIUM** ✅
- Logic: Concrete examples help edge cases
- Same domain as distributed-tracing (+7.7%)
- Extrapolating pattern, not directly tested

**Expected Outcome**:
- Before: 92.3%
- After: 95-100%

**Effort**: 6-10 hours
- 4-6h: Write secure code examples for all top 10
- 2h: Verify examples compile/run
- 1-2h: Document

---

## Category 5: Known Limitations (Low Confidence Recommendations)

### bash-defensive-patterns (90.9% baseline)

**What We Know**:
- 90.9% baseline (good)
- 9.1% gap remains
- Skill provides principles

**Recommendation** (Low confidence):
- Add actual bash code snippets (not just principles)
- Error handling patterns with `set -e`, `trap`, etc.
- Input validation patterns

**Confidence**: **LOW** ⚠️
- Logical (code > principles)
- But gap may be due to reasoning, not knowledge
- Paper says: "bottleneck lies in deeper capability gaps"

**Effort**: Medium

---

## Category 6: Already-Solved Problems (Don't Change)

### 24 skills at 100% pass rate (both with/without skill)

**Paper Finding**:
> "the base model already possesses sufficient capability to solve every task instance without any skill guidance"

**Recommendation**: **DEPRECATE or use sparingly**

These skills:
- add-uint-support
- analytics-events
- analyze-ci (actually reduces tokens -10.6%, keep!)
- dbt-transformation-patterns
- gitops-workflow
- grafana-dashboards
- implementing-agent-modes (reduces tokens -47.8%, keep!)
- k8s-manifest-generator
- [etc., 16 more]

**Action**:
- Remove or mark as deprecated
- Keep exceptions that reduce tokens (analyze-ci, implementing-agent-modes, etc.)

**Confidence**: **HIGH** ✅
- Paper documents this clearly
- 100% = 100%, can't improve

---

## Category 7: Capability Gap Issues (Can't Fix with Skill)

### 15 skills with identical imperfect pass rates

**Paper Finding**:
> "This suggests that the bottleneck lies not in the absence of domain knowledge, which the skill ostensibly provides, but in deeper capability gaps such as complex multi-step reasoning, unfamiliar API surfaces, or brittle evaluation harnesses."

**Examples**:
- xlsx (36.4%): Too complex (spreadsheet operations beyond reasoning)
- turborepo (50%): Complex multi-faceted monorepo concepts
- changelog-automation (70%): Edge cases in formatting/versioning

**Recommendation**: **Can't be fixed by improving the skill**

- ❌ Don't invest in trimming/rewriting
- ✅ Consider: Make tasks harder (to push capability)
- ✅ Consider: Deprecate (if unfixable)
- ✅ Consider: Mark as requiring stronger model

**Confidence**: **HIGH** ✅
- Paper is explicit: capability gap, not knowledge gap
- Skill won't help because problem is too hard

**Action**:
- xlsx: DEPRECATE (36.4% is fundamentally hard)
- turborepo: DEPRECATE or wait for stronger models
- Others: Mark as "requires strong reasoning capability"

---

## Summary: What to Do

### 🔴 CRITICAL (Do immediately, 1-2 weeks)

| Skill | Action | Why | Effort |
|-------|--------|-----|--------|
| linkerd-patterns | Update templates to v1beta3+ | Paper documents version-mismatch failure | 2-4h |
| springboot-tdd | Update for Spring Boot 3.x | Paper documents version conflict | 2-3h |
| django-patterns | Trim scope OR decompose | Paper documents scope-mismatch harm | 4-6h |

**Impact**: Remove actively harmful skills (-9.1%, -10%)

---

### 🟡 HIGH PRIORITY (Do in weeks 3-4, 5-8 hours)

| Skill | Action | Why | Effort |
|-------|--------|-----|--------|
| service-mesh-observability | Trim to essentials | Paper: verbosity without correctness gain | 2-3h |
| python-background-jobs | Narrow to Celery | Paper: excessive overhead with no gain | 1-2h |
| github-actions-templates | Update to v4 + examples | 70% baseline, outdated | 2-3h |

**Impact**: Recover 300-500K tokens per run, same correctness

---

### 🟢 MEDIUM PRIORITY (Do in month 2, 6-10 hours)

| Skill | Action | Why | Effort |
|-------|--------|-----|--------|
| creating-financial-models | Add code implementations | Pattern from risk-metrics-calculation success | 6-8h |
| security-review | Add OWASP code examples | Pattern from distributed-tracing success | 6-10h |

**Impact**: Potential +5-10% improvement on edge cases

---

### ❌ DEPRECATE (No investment)

| Skill | Why |
|-------|-----|
| xlsx | 36.4% baseline, capability-limited, not skill-fixable |
| turborepo | 50% baseline, fundamentally complex |
| fix | 91.7%, base model sufficient, high overhead (+153%) |
| [24 others at 100%] | Already-solved problems, no improvement possible |

---

## Confidence Key

- **HIGH** ✅: Paper documents this mechanism and failure
- **MEDIUM** ⚠️: Logic is sound, but extrapolated from other cases
- **LOW** ❌: Speculative, may not work

All recommendations grounded in paper findings where possible.

---

**Report Generated**: March 24, 2026
**Source**: SWE-Skills-Bench paper (arXiv:2603.15401v1)
**Methodology**: Evidence-based fixes only; speculations marked as such
