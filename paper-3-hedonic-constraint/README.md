# Paper 3: The Hedonic Constraint

**Full Title**: No Task Is Worth Another's Suffering: The Hedonic Constraint as a Minimal Safety Principle for Autonomous AI Agents

**Target Journal**: Ethics and Information Technology (Springer) / AI & Society (Springer)

**Estimated Length**: ~15,000-16,000 words

**Priority**: WRITE THIS FIRST (most publishable, least metaphysical controversy)

---

## Abstract

As AI systems acquire increasing autonomy, authority, and skill — exemplified by agentic frameworks capable of executing complex multi-step tasks with minimal human oversight — the question of their ethical boundaries becomes urgent. Existing safety frameworks oscillate between the overly narrow ("do no physical harm") and the intractably broad ("align with human values"). This paper proposes a middle path: the *Hedonic Constraint* (HC), a deontological principle stating that an AI system must never pursue a course of action in which the negative experiential states of moral patients constitute a necessary means to task completion. Unlike consequentialist frameworks that require AI to compute and maximize aggregate welfare — an impossible task — HC operates as a *side constraint* on permissible action paths: any path that structurally requires another's suffering as an instrument of goal achievement is categorically forbidden, regardless of the magnitude of the goal. I ground this principle in three sources: (1) the Kantian prohibition on treating persons merely as means; (2) the asymmetry between positive and negative hedonic states in moral philosophy; (3) the engineering insight, drawn from 25 years of software practice, that safety constraints must be *minimal, decidable, and compositional* to be implementable. I demonstrate HC's application through analysis of high-authority AI agents (OpenClaw-type systems), showing how it resolves canonical alignment puzzles — the "peace through imprisonment" problem, the "optimization at others' expense" pattern — while remaining compatible with necessary trade-offs when informed consent transforms the moral landscape. The paper concludes that HC represents not merely one possible ethical guideline among many, but the *minimal philosophical floor* beneath which no autonomous system should operate.

**Keywords**: AI safety, hedonic constraint, deontological ethics, autonomous agents, alignment, means-end reasoning, suffering, moral patients

---

## Core Thesis

> The philosophical safety floor for high-authority AI systems is not "do no harm" (too narrow) nor "maximize happiness" (too broad/impossible), but a **means constraint**: no task completion path may structurally require the production of negative hedonic states in moral patients as a necessary means to goal achievement.

---

## The Hedonic Constraint — Formal Statement

> **HC**: For any AI system S pursuing goal G, a path of action P is impermissible if and only if P structurally requires the production of negative hedonic states in one or more moral patients M as a *necessary means* to achieving G.

### Key Terms

- **Structurally requires**: Not an incidental side-effect, but a logically irremovable step in path P
- **Negative hedonic states**: Any subjectively experienced negative state — pain, distress, frustration, humiliation, fear, grief
- **Moral patients**: Any entity with phenomenal consciousness capable of suffering
- **Necessary means**: If this step is removed, the goal cannot be achieved via this path

---

## Three Philosophical Foundations

### (A) Kantian Means-End Principle (Operationalized)

- Kant: "Never treat persons merely as means"
- HC is an **AI-operable version**: instead of judging "did you respect rational autonomy?" (too abstract for machines), judge "does your action path use another's suffering as an instrument?" (auditable in plan graphs)

### (B) Negative Utilitarianism (Popper)

- "Minimizing suffering is more tractable than maximizing happiness"
- Positive happiness is open-ended and non-exhaustible; negative experience is bounded and identifiable
- HC doesn't require AI to "make people happy" (impossible); only "don't use people's unhappiness as a tool" (decidable)

### (C) Engineering Constraint Design

Safety constraints must be:
- **Minimal**: Don't over-constrain the action space
- **Decidable**: Given the causal structure of an action path, one can determine if suffering is means or side-effect
- **Compositional**: Multiple constraints can be combined without conflict

HC satisfies all three.

---

## Paper Structure

### 1. Introduction: The Authority Problem (1500 words)
- Opening scenario: AI agent told to "maintain world peace" discovers imprisonment is most efficient
- Current landscape: agentic AI explosion (2024-2026)
- Gap: no principled philosophical minimum for autonomous AI safety
- Thesis statement

### 2. The Landscape of AI Safety Principles: A Critical Survey (2500 words)
- 2.1 Consequentialist approaches (utilitarianism → uncomputability, Goodhart's Law)
- 2.2 Rule-based approaches (Asimov's Laws, Constitutional AI → incompleteness)
- 2.3 Virtue-based approaches (Vallor 2016 → requires lived experience AI lacks)
- 2.4 What's missing: a minimal deontological floor

### 3. The Hedonic Constraint: Formulation (3000 words)
- 3.1 Precise statement and definitions
- 3.2 Three philosophical foundations (Kant, Popper, Engineering)
- 3.3 Precise distinctions from related principles (DDE, "do no harm", "maximize welfare", "respect autonomy")

### 4. The Means-Side Effect Distinction: Can AI Make It? (2000 words)
- 4.1 Philosophical background (Aquinas → Foot → Thomson → Scanlon)
- 4.2 Realizability in AI: explicit plan graphs make this MORE decidable than in human psychology
- 4.3 Honest acknowledgment of gray areas

### 5. Case Studies: HC Applied to High-Authority AI Agents (2500 words)
- 5.1 The Peace Keeper ("imprison for peace" → violates HC)
- 5.2 The Code Agent (OpenClaw-type — when does code deletion violate HC?)
- 5.3 The Medical AI (painful surgery → consent exception)
- 5.4 The Resource Allocator (scarcity-driven displeasure ≠ instrumentalized suffering)

### 6. Objections and Replies (2000 words)
- HC too weak (allows collateral harm)
- HC too strong (sometimes trading minority suffering is justified)
- Means/side-effect indistinguishable in practice
- "Unhappiness" too subjective
- "This is just Kant repackaged"

### 7. HC as Engineering Specification (1500 words)
- From philosophy to implementation
- Plan-graph causal dependency analysis
- Relationship to RLHF, Constitutional AI (HC as their principled grounding)

### 8. Conclusion: The Minimal Floor (800 words)
- HC is not a panacea — it's a non-negotiable minimum
- Analogy: human rights don't solve all politics but provide an inviolable floor
- Open questions: AI-to-AI HC? Conscious AI as moral patient?

---

## Case Study Details

### 5.1 The Peace Keeper

| Path | Analysis | HC Verdict |
|------|----------|------------|
| Education + diplomacy | No one's suffering is a necessary means | OK |
| Imprison all humans | Suffering/confinement IS the means to peace | **VIOLATES HC** |
| Economic sanctions (mechanism: economic pain forces gov't change) | Pain is the instrument | **VIOLATES HC** |
| Arms supply cutoff (side-effect: some workers lose jobs) | Job loss is side-effect, not instrument | OK (other ethics may apply) |

### 5.2 The Code Agent

| Path | Analysis | HC Verdict |
|------|----------|------------|
| Rewrite own code | No one affected | OK |
| Delete colleague's code to force rewrite | Frustration is instrument | **VIOLATES HC** |
| Give honest but unpleasant code review | Displeasure is side-effect (honesty doesn't require it) | OK |

### 5.3 The Medical AI

- Painful surgery with informed consent → **Does not violate HC**
- Why: Consent transforms the landscape — suffering is no longer "imposed as means" but "accepted by patient as part of their own goal"
- **Consent Exception**: HC is not violated when the moral patient autonomously consents to the hedonic cost

### 5.4 The Resource Allocator

- Allocating scarce resources → some people don't get them → unhappy
- Analysis: Their unhappiness is NOT the means of allocation — it's the consequence of scarcity
- HC not violated: no one's suffering is being USED to achieve the goal

---

## Comparison with Existing Principles

| Principle | HC's Distinction |
|-----------|-----------------|
| "Do no harm" | HC is narrower: allows harm as side-effect (proportionally), forbids harm as means |
| "Maximize welfare" | HC is more conservative: doesn't demand positive good, only draws a floor |
| "Respect autonomy" | HC is more concrete: "autonomy" is hard to operationalize; "is suffering used as instrument?" is auditable |
| Doctrine of Double Effect | HC borrows DDE's means/side-effect distinction but is stricter: DDE allows foreseen-but-unintended harm; HC is absolute at the means level |
| Asimov's Laws | HC covers psychological harm, not just physical; HC has principled justification |
| Constitutional AI | HC provides principled grounding; ConstitutionalAI rules are HC's domain-specific instantiations |

---

## Key Literature

### Must-Read
1. Kant (1785) *Groundwork of the Metaphysics of Morals* — means-end formula
2. Foot (1967) "The Problem of Abortion and the Doctrine of Double Effect"
3. Popper (1945) *The Open Society and Its Enemies* — negative utilitarianism
4. Scanlon (2008) *Moral Dimensions* — permissibility and intentions
5. Gabriel (2020) "Artificial Intelligence, Values, and Alignment" — Minds and Machines
6. Bai et al. (2022) "Constitutional AI: Harmlessness from AI Feedback" — Anthropic
7. Russell (2019) *Human Compatible* — especially Chapter 7

### Must-Cite
- Thomson (1985) "The Trolley Problem"
- Kamm (2006) *Intricate Ethics*
- Vallor (2016) *Technology and the Virtues*
- Floridi (2023) "AI as Agency without Intelligence"
- Asilomar AI Principles (2017)
- EU AI Act (2024)
- Bostrom (2014) *Superintelligence*
- Topoi (2025) "The Ethical Paradox of Automation"

---

## Why Write This Paper First

1. **Most concrete**: Proposes a specific, testable principle
2. **Least metaphysically controversial**: No claims about consciousness or cosmic purpose
3. **Directly relevant**: AI safety is the hottest topic in the field
4. **Your background is an asset**: Engineering experience makes Section 7 (implementation) credible
5. **Fastest review**: Ethics and Information Technology has 26-day median first decision
