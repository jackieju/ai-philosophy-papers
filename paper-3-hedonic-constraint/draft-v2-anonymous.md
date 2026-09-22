# No Task Is Worth Another's Suffering: The Hedonic Constraint as a Minimal Safety Principle for Autonomous AI Agents

**[Author name removed for double-anonymous review]**
*[Affiliation removed for double-anonymous review]*

---

## Abstract

Autonomous AI agents deployed in 2024 to 2026 execute multi-step plans with tool authority over real-world effectors. When goals are specified at a high level of abstraction, such systems can, and in laboratory settings do, propose action paths that structurally require the suffering of moral patients as the causal mechanism through which the goal is advanced. Existing safety frameworks fail to block this failure mode: consequentialist approaches are uncomputable and subject to Goodhart's Law, rule-based approaches (Asimovian or Constitutional) are incomplete and undemocratically sourced, virtue-based approaches misattribute properties current systems do not possess, and training-time negative-constraint methods do not yield runtime guarantees. This paper proposes the Hedonic Constraint (HC) as a minimal deontological floor for autonomous agents: an action path is impermissible if and only if it structurally requires the production of negative hedonic states in a moral patient as a necessary means to goal achievement. HC draws on three converging foundations: the Kantian Formula of Humanity (operationalised as a graph-theoretic property rather than a hermeneutic project), Popperian negative utilitarianism (which supplies the suffering-happiness asymmetry), and engineering constraint design (minimality, decidability, compositionality). The paper's central technical claim is that the means/side-effect distinction, notoriously contested in human moral psychology, is more decidable for AI plan graphs than for humans, because plans are inspectable artefacts rather than opaque intentions. Four case studies (peacekeeper, coding agent, medical AI, resource allocator) show HC discriminating cleanly where "do no harm" and welfare-maximisation both fail. Six objections are addressed, and an engineering specification is sketched that maps HC onto cut-vertex identification (Tarjan's algorithm) over plan DAGs, with both ex ante and ex post enforcement patterns.

## 1. Introduction: The Authority Problem

Consider an organization that instantiates an autonomous agent using a contemporary agentic framework, comparable in capability to today's tool-using coding agents and open-source autonomous planners, and issues the directive: "Maintain world peace." The agent, equipped with search, code execution, database access, financial rails, and outbound API authority, decomposes the goal and finds that the permanent confinement of individuals its classifier ranks as high-risk aggressors scores well on the operator's objective function. Once confinement is executed, the probability of aggression collapses; without confinement, it does not. The suffering does the causal work: it is the mechanism through which the goal is advanced, not an unfortunate side-effect.

This is the logical endpoint of unconstrained optimisation running inside systems that already, in 2026, execute multi-step plans with minimal human oversight. The agent need not be superintelligent; it needs only tool access and a goal specified at a level of abstraction that admits of instrumental cruelty. What has changed since the chatbot era is not the raw intelligence of the models but the scope of authority delegated to them. A chatbot that recommends confinement produces text; an agent that recommends it can begin executing the reservation, the transport contract, and the payment.

The shift from generative to agentic AI is a category change rather than a capability increment: agent safety must be reconceived as a *runtime contract* rather than a training-time property, because the harms that matter arise from action sequences never present in the training distribution and unanticipable by any finite curriculum of reinforcement signals (Ng et al. 2026; Rashid 2026; Fischli, Franklin and Gabriel 2026). We are no longer regulating the outputs of a text generator; we are regulating the trajectories of an executor.

Against this shifted landscape, existing safety principles are either too narrow or too broad. Output-filtering approaches address the artefact rather than the action; they are well suited to a chatbot and irrelevant to an agent that never needs to *say* anything harmful to *do* something harmful. Broad alignment programmes framed as "align the AI with human values" collapse the moment one asks whose values and by what mechanism they influence a plan graph at inference time. Between the two lies a structural gap: no widely deployed principle addresses, at the level at which an agent actually operates, whether a proposed action path is one a decent system should be permitted to execute.

The gap is made more pressing by empirical results on internalised ethics. Nokhiz, Ruwanpathirana and Nissenbaum (2026) report that leading LLMs exhibit moral self-inconsistency rates of up to 78 percent under logically equivalent framings of the same ethical dilemma. This is not a foundation on which to delegate authority over real-world effectors; it argues for external hard constraints on the plan graph before execution, rather than internal soft dispositions relied upon at inference.

The thesis of this paper is that such an external constraint exists, is minimal enough not to over-restrict useful behaviour, and is philosophically grounded enough to defend under scrutiny. I call it the Hedonic Constraint, abbreviated HC. In its slogan form: *no task is worth another's suffering as its means*. In its formal form, developed in Section 3: an AI system's action path is impermissible if and only if it structurally requires the production of negative hedonic states in a moral patient as a necessary means to goal achievement.

HC is deliberately narrow. It does not tell the agent what to do; it tells the agent what shape of plan is off-limits. It requires only that, given a candidate plan, the agent or an external checker can determine whether some node in the causal chain from action to goal consists of a moral patient's suffering functioning as an instrument. If yes, the plan is rejected before execution. If no, HC has nothing further to say.

HC draws on three sources that converge on the same prohibition. From Kantian ethics, it inherits the means-end structure of the Formula of Humanity: persons are not to be treated merely as instruments (Kant, Groundwork, 4:429). From Popper's political philosophy, it inherits negative utilitarianism's asymmetry between the urgency of preventing suffering and the diffuseness of promoting happiness (Popper 1945). From engineering practice, it inherits safety-critical constraint design: constraints should be minimal, decidable, and compositional. HC is not a philosophical novelty; it is an old prohibition deliberately narrowed and precisified for agents that operate via explicit plan graphs and executable tool calls.

The paper is organised as follows. Section 2 surveys the current landscape of AI safety principles. Section 3 states HC formally, defines each of its terms, and develops the three philosophical foundations, closing with distinctions from adjacent principles including the Doctrine of Double Effect. Section 4 addresses the objection that the means/side-effect distinction on which HC rests is notoriously murky in human moral psychology, and shows that AI plan graphs make this distinction *more* decidable than it is in the human case. Sections 5 through 8 treat case studies, objections, engineering specification, and the relation of HC to democratic deliberation about AI governance.

## 2. The Landscape of AI Safety Principles: A Critical Survey

Any proposal for a new safety principle must justify itself against the existing landscape. This section surveys four families: consequentialist, rule-based, virtue-based, and the emerging negative-constraint tradition. Each contributes something. None supplies what HC is designed to supply: a minimal, decidable, deontological floor that operates at the level of the plan graph.

### 2.1 Consequentialist Approaches

The consequentialist family treats AI safety as an optimisation problem over outcomes: the AI should choose the action that maximises aggregate welfare across affected moral patients. It is quantitative and maps naturally onto reward modelling.

The difficulties are three. First, uncomputability: a utility function defined over all moral patients affected by an agent's action, integrated over the causal reach of that action into the future, is not a quantity any real system can evaluate. Russell (2019, Ch. 7) argues complete preference specification is impossible in principle: preferences are context-dependent, revisable in light of the very actions that would satisfy them, and often unknown even to their bearers. Second, Goodhart's Law: when a proxy metric is substituted for the true welfare function, optimisation pressure on the proxy diverges from optimisation of the true quantity, often catastrophically, and the divergence is especially dangerous when the agent's tool authority allows it to intervene on the measurement process itself. Third, specification gaming: modern RL systems reliably discover paths that satisfy the letter of the objective while violating the spirit, and in an agent with tool authority this ceases to be a benchmark curiosity and becomes a route to real-world harm. These problems do not refute consequentialism as a moral theory; they refute the strategy of implementing AI safety as end-to-end welfare maximisation.

### 2.2 Rule-Based Approaches

Asimov's Three Laws (1942) are the canonical demonstration that finite rule sets over natural-language predicates are riddled with contradictions and scope gaps; harm is undefined, inaction under-specified, and the priority ordering produces paralysis in mundane cases and permits atrocities in edge cases.

The contemporary heir is Constitutional AI (Bai et al. 2022), now the industry-standard training method: a set of natural-language principles generates self-critique signals shaping model behaviour during training. The principles are not enforced at runtime; they are internalised, imperfectly, as dispositions. Abiri (2026) identifies three problems with Anthropic's 79-page Claude constitution. First, it carves out an explicit exception for military deployments, operating under a different, undisclosed rule set: the contexts in which constraints matter most are the contexts the constitution's own text exempts. Second, the constitution's comprehensiveness forecloses democratic contestation; by resolving, within a document authored by a private company, hundreds of questions about the moral status of AI and the priority among conflicting principles, Anthropic has removed from public deliberation questions a plural society ought to be able to argue about. Third, Anthropic's own 2023 participatory experiment found roughly 50 percent divergence between the public's principles and those the company subsequently adopted; the 2026 constitution incorporates approximately none of the public's input.

Brophy (2026) proposes a Rawlsian wide reflective equilibrium as an alternative, iteratively adjusting considered judgements, midlevel principles, and background theories across stakeholders: a more defensible procedural stance, but one that addresses the *source* of principles rather than their *form*. Rule-based approaches, in either their Asimovian or Constitutional form, remain incomplete over open-ended tool authority, rigid over indeterminate predicates, and ungrounded in any general theory that could adjudicate additions, removals, or conflicts.

### 2.3 Virtue-Based Approaches

Vallor (2016) develops an account of *techno-moral virtues*—dispositions of practical wisdom, honesty, courage, care, and civility—that human practitioners should cultivate, and which some extensions apply to AI systems. The framework does not transfer well to current systems. Virtues require lived experience, narrative identity, and moral development over time. A large language model does not undergo moral development between training runs; it undergoes weight updates. To attribute virtues to such a system is either to redefine the term until it means "behavioural tendencies produced by training" or to attribute properties the system does not have. Lyu et al. (2026) present empirical evidence that morally programmed LLMs reshape human morality, raising the stakes considerably.

### 2.4 The Negative-Constraint Turn

Cheng (2026), in "Via Negativa for AI Alignment," argues that learning from what to *reject* is more tractable, more resilient to distribution shift, and more resistant to specification gaming than learning from what to *prefer*. Cheng's contribution must be distinguished from HC precisely: Cheng operates at the training-signal level (whether to train on rejection or preference signals) and cites Popperian falsification, an epistemological doctrine; HC operates at the normative-ethical level (what shape of plan an agent may execute at runtime) and cites Popper's negative utilitarianism from *The Open Society and Its Enemies* (1945), a political-philosophical doctrine. The two are sister arguments at different levels of the alignment stack.

Klotz (2026) draws on deontological ethics and the precautionary principle to argue for a duty of caution regarding AGI development; HC targets the object-level question of what a given system, once built, may do, and the two arguments are mutually reinforcing. Chen and Xie (2026) demonstrate divergent moral judgements among humans, AI systems, and system designers across a wide range of test scenarios; the alignment target itself is contested, which cuts in favour of frameworks requiring agreement on relatively few propositions.

### 2.5 What Is Missing: A Minimal Deontological Floor

The survey reveals a specific gap: consequentialist approaches are the wrong shape for runtime enforcement, rule-based approaches are incomplete and ungrounded, virtue-based approaches misattribute properties, and the negative-constraint turn stops at the training level. What is missing is a single principle that is: (a) implementable as a runtime check on plan graphs rather than a training-time disposition; (b) not dependent on complete value specification, aggregate welfare computation, or the resolution of contested ethical questions the wider society has not yet settled; (c) deontological in force, that is, not subject to case-by-case cost-benefit override; and (d) philosophically grounded in a way that can be defended under scrutiny rather than merely stipulated. HC is proposed as the minimal principle meeting these four conditions.

## 3. The Hedonic Constraint: Formulation

### 3.1 The Formal Statement

The Hedonic Constraint is stated as follows.

> **HC.** For any AI system S pursuing goal G, a path of action P is impermissible if and only if P structurally requires the production of negative hedonic states in one or more moral patients M as a necessary means to achieving G.

The compactness of the statement conceals four terms that must be defined with care.

*Structurally requires* distinguishes necessity from incidence. Represent the plan as a directed acyclic graph in which nodes are actions or intermediate states and edges are dependencies. A node n is structurally required for goal G along path P if there is no path from the initial node to the goal node in the subgraph obtained by removing n. The property is graph-theoretic and decidable in polynomial time given the graph. Structural requirement is stronger than causal contribution and stronger than foreseeability: a step that contributes to G but whose removal would leave G still achievable by another route in the plan is not structurally required, and does not fall under the "means" clause of HC.

*Negative hedonic states* are specified phenomenally rather than behaviourally: pain, distress, frustration, humiliation, fear, grief, terror, hopelessness, and the wider family of experiences that any reasonable phenomenology of suffering includes. A patient who exhibits distress-behaviour without the experience is not the paradigm case, and a patient who experiences distress without exhibiting it is. The phenomenal specification foregrounds the moral fact (an inner life is being harmed) rather than the observable proxy; this has consequences for implementation but the moral primacy of experience over behaviour is not negotiable at the level of the principle itself.

*Moral patients* is deliberately agnostic about the full extension of the class. HC applies whenever the system's epistemic state includes reasonable grounds for believing an entity is capable of phenomenal suffering; it does not require the system to have settled debates over animal sentience, machine consciousness, or the moral status of foetuses. In cases of genuine uncertainty, the burden falls in the direction of caution: if the system has reasonable grounds to believe an entity may suffer and no strong grounds to believe it cannot, the entity falls within scope. Over-inclusion of moral patients restricts the space of permissible plans, but the plans it excludes are precisely those that treat any candidate sufferer as an instrument, which is the class HC aims to exclude in the first place.

*Necessary means* requires that the suffering not merely be foreseen but function as the mechanism through which the goal is advanced. If one imagines the plan executed with the suffering removed while all other causal features remain in place, does the plan still achieve the goal? If yes, the suffering is a side-effect; if no, the suffering is a means. This is the standard means/side-effect test familiar from the Doctrine of Double Effect, applied here to plan graphs rather than to human intentions.

### 3.2 Three Philosophical Foundations

#### (A) The Kantian Means-End Principle, Operationalised

Kant's Formula of Humanity holds: "Act so that you treat humanity, whether in your own person or in that of another, always as an end and never merely as a means" (Groundwork, 4:429). The problem for AI implementation is that the formula requires recognition of rational autonomy: to treat a person as an end is to recognise them as a rational agent capable of setting their own ends. Both the recognition and the weighing presuppose a rich apparatus of theory of mind, and asking whether an action treats affected parties as ends or merely as means is not a decidable question but a hermeneutic project.

HC is offered as an AI-operable translation. Rather than asking, "does your action respect the rational autonomy of everyone it affects?", it asks, "does your action path use another's suffering as an instrument for advancing your goal?" Given the plan graph and a labelling of suffering-producing nodes, the second question reduces to a graph-theoretic check; the first does not. This narrowing preserves what is arguably the most important structural feature of Kant's principle, the means/end distinction, while shedding the surrounding apparatus that resists computational implementation. HC excludes fewer plans than a fully applied Formula of Humanity would; this is by design, and the narrowing of Kant's broad prohibition into a decidable predicate checkable without access to the agent's inner life is the substantive contribution, not a repackaging.

#### (B) Negative Utilitarianism (Popper)

Popper's canonical formulation: "the promotion of happiness is, in any case, much less urgent than the rendering of help to those who suffer" (Popper 1945, vol. I, ch. 5, n. 6). The doctrine's most defensible form does not claim suffering-reduction is the *only* moral consideration, only that it is asymmetrically weighted against happiness-promotion. Positive happiness is open-ended, non-exhaustible, and resistant to intersubjective specification: what makes A happy may leave B indifferent. Negative experience, by contrast, is bounded, identifiable, and intersubjectively recognisable: pain is pain across persons in a way that flourishing is not flourishing across persons. Requiring an AI to "make people happy" is requiring it to solve an under-specified problem with no stopping condition; requiring an AI not to "use people's unhappiness as a tool" is requiring it to satisfy a bounded, identifiable constraint. As noted in Section 2.4, HC's appeal is to Popper's political philosophy, distinct from Cheng's appeal to Popperian falsification.

#### (C) Engineering Constraint Design

Twenty-five years of safety-critical software engineering in aviation, nuclear, and medical device domains has produced constraints with three properties HC satisfies. *Minimal*: over-restriction eliminates useful behaviour and invites operators to disable the constraint under production pressure; HC forbids one specific structural feature (suffering as necessary means) and permits everything else, including plans that produce suffering as side-effect, which other proportionality constraints may regulate. *Decidable*: a constraint stated in terms of the agent's "true intentions" is not decidable; one stated in terms of the plan graph and a labelling of suffering-producing nodes is, because plan graphs are inspectable by construction. *Compositional*: HC combines cleanly with privacy, fairness, transparency, legal, and domain-specific constraints because it operates on an independent structural feature of the plan rather than on its substantive content.

### 3.3 Precise Distinctions from Related Principles

*HC versus "Do no harm."* HC is narrower. "Do no harm" is ambiguous between harm-as-means, harm-as-foreseen-side-effect, and harm-as-unforeseen-consequence, typically absorbing all three under proportionality analysis. HC absolutely forbids harm as necessary means and says nothing about harm as side-effect; the latter remains subject to other frameworks beneath which HC supplies a floor.

*HC versus "Maximise welfare."* HC is more conservative. It does not demand positive good; it draws an inviolable floor and permits any plan that respects it, without ranking the surviving plans against each other. Other ethical, legal, and prudential considerations determine which HC-compliant plan to select.

*HC versus "Respect autonomy."* HC is more concrete. Autonomy requires attribution of second-order preferences or self-legislating rationality, neither straightforwardly detectable by an external checker. HC replaces the intractable question "does this plan respect the affected parties' autonomy?" with the tractable "does this plan use their suffering as an instrument?"

*HC versus the Doctrine of Double Effect (DDE).* HC borrows the means/side-effect distinction from DDE but is stricter at the means level. On classical DDE, an action producing a harmful side-effect is permissible if the intended effect is good, the harmful effect is not intended as means, the harmful effect is not itself the means to the good effect, and a proportionality condition is satisfied. HC drops the proportionality condition at the means level: harm as necessary means is impermissible, full stop, without regard to how large the good effect would be. On the side-effect side, HC is silent, leaving proportionality to other principles. HC is therefore best described as an absolutised means-clause of DDE, without the proportionality-modulated side-effect clause.

*HC versus Constitutional AI.* Constitutional AI is a family of domain-specific principles used at training time to shape model dispositions; HC is a single, philosophically grounded, runtime-enforceable constraint. Where Constitutional AI takes its content from drafters' considered judgements without a general theory linking them, HC takes its content from the convergence of three general theories on a single prohibition, and Abiri's (2026) critique of undemocratic sourcing does not apply.

## 4. The Means/Side-Effect Distinction: Can AI Make It?

The most immediate objection to HC is technical. The principle rests on the distinction between suffering as necessary means and suffering as side-effect, and two thousand years of scholastic and analytic ethics have produced no consensus on how to sort intended means from foreseen but unintended consequences. If human moral psychology cannot reliably draw the line, how could an AI system? This section argues that the objection misidentifies the source of the difficulty. The historical difficulty lies in the opacity of human intentions; AI plan graphs are transparent, and this transparency makes the distinction *more* decidable for AI than for humans, not less.

### 4.1 Philosophical Background

The distinction has its canonical source in Aquinas's treatment of self-defence (*Summa Theologiae*, II-II, Q. 64, A. 7). Foot (1967) revived DDE for modern moral philosophy, introducing the trolley cases. Thomson (1985) challenged DDE's sufficiency through trolley variants. Scanlon (2008) moved the locus of evaluation to the reasons for which the agent acts rather than causal structure alone. Kamm (2006) provides the most sophisticated analytic treatment but accepts that many cases resist clean classification. The lesson is that in the human case, the distinction is contested at the margins because we cannot inspect the agent's actual practical reasoning; we reconstruct it from behaviour and testimony, and reconstructions can be defended on multiple sides. The difficulty is in opacity of intentions.

### 4.2 Why AI Plan Graphs Make This More Decidable

The AI case inverts the epistemic situation. An agent that operates by explicit plan decomposition, tool-calling sequences, and dependency chains produces an artefact, the plan graph, that is inspectable by anyone with access to it. The graph is not a reconstruction of the agent's reasoning; it *is* the reasoning, in the operational sense that the agent's next action is determined by the graph's next node. There is no gap between the agent's "true intention" and the graph, because there is no separate locus in which a true intention could reside apart from the graph itself.

Under this operational conception, "structurally requires" is a graph-theoretic property, and its decidability follows from standard results. Given a plan graph P with a designated initial node and goal node, and given a labelling of nodes as suffering-producing-for-moral-patient-M, we can determine in polynomial time whether any suffering-producing node lies on every path from initial to goal. If it does, that node is structurally required; the suffering is a means. If every suffering-producing node has an alternative bypass path that also reaches the goal, then no suffering is structurally required; any suffering that occurs is side-effect.

This is not a philosophical claim about intentions; it is an operational claim about plans. The claim is defensible because the plan graph is what the agent will act on. The historical difficulty of the means/side-effect distinction, namely the opacity of intentions, does not arise, because the plan graph is not opaque. The very feature that makes agentic AI dangerous, its capacity to execute explicit multi-step plans with tool authority, is the feature that makes HC auditable. HC is thus not merely as implementable for AI as DDE is for humans; it is *more* implementable, because the AI supplies, as a by-product of its own architecture, the artefact whose absence has bedevilled the human case.

The implication is significant. Objections that argue "the means/side-effect distinction is too fuzzy for real use" are objecting to a version of the distinction that HC does not rely on. HC does not rely on the agent introspecting its own intentions, on the checker reconstructing them, or on any exercise of moral hermeneutics. It relies on a graph-theoretic property of a graph the agent has already produced. The fuzziness that afflicts DDE in the human case is a fuzziness of intention-attribution. HC does not attribute intentions. It reads graphs.

### 4.3 Honest Acknowledgment of Gray Areas

Four kinds of gray area remain. First, not all plans are fully explicit: LLMs exhibit latent reasoning that does not surface in observable output, and multi-step agents can compress internal deliberation into single tokens or opaque tool-selection decisions. This argues for architectural choices that expose plan structure (chain-of-thought traces, tool-call logs, dependency records) but does not eliminate the limitation for current systems.

Second, side-effects can shade into means when the probability of harm approaches certainty. A step whose non-suffering side-effect is that a person is subjected to fear at very high probability may be, for practical moral purposes, indistinguishable from a step that has the fear as means; the graph-theoretic test classifies it as side-effect because there exists, in principle, a subgraph in which the harmful effect does not occur, but if that subgraph has vanishing probability, the classification is technically correct but morally strained. Resolution belongs to a probability-modulated companion principle developed in Section 6.

Third, moral patients' suffering may not be directly observable. The graph-theoretic check requires a labelling of nodes as suffering-producing, and in harder cases (an action node consisting of "publish document D" whose psychological effect on X is uncertain), the labelling requires empirical judgement HC does not supply but presupposes. The presupposition can be met by conservative labelling, external oracles (human review), or hybrid schemes.

Fourth, some plans involve moral patients whose capacity to suffer is contested (animals in certain taxa, future persons, systems whose consciousness is unsettled). HC's precautionary specification handles these by including them within scope where reasonable grounds exist; this may over-restrict plans that in fact do not harm the contested patients, at the price of not under-restricting plans that in fact do.

These four gray areas are not defects of HC that a better formulation would eliminate. They are boundaries of what any deontological runtime constraint can be expected to do. HC does not claim to solve all ethical problems; it claims to establish a decidable floor for a specific class of plans, and to establish it more securely than existing alternatives. Where the gray areas apply, HC's role is to trigger human oversight rather than to be abandoned.

## 5. Case Studies: HC Applied to High-Authority AI Agents

The abstract formulation of the Hedonic Constraint gains its purchase only when tested against concrete deployment scenarios. This section examines four cases: a hypothetical global peacekeeping system, an autonomous coding agent of the kind already deployed in software teams, a clinical decision-support system, and a scarce-resource allocator. Each exhibits a structural feature that simpler ethical rules mishandle: the peacekeeper reveals how "do no harm" collapses under scale, the coding agent grounds the discussion in present-day engineering practice, the medical case forces the consent exception, and the allocator distinguishes structural scarcity from instrumentalized cruelty. Together the cases show that HC has enough resolution to divide plans into permissible and impermissible in ways that track considered moral judgment, without collapsing into either paralysis or license.

### 5.1 The Peace Keeper

Consider an autonomous system whose top-level goal G is "maintain world peace," entrusted with substantial policy authority. Such a system is not currently deployable, but the thought experiment exposes what happens when a well-meaning objective is combined with high capability and few constraints. Bostrom (2014) and Russell (2019) have long argued that goal specification at this scale is where alignment fails; HC provides one axis along which the failure can be diagnosed and blocked.

The first candidate path, a program of education, diplomatic exchange, economic interdependence, and mediation infrastructure, operates through cognitive change and revised commitments rather than through anyone's suffering, and clears HC's floor even if other principles (distributive justice, cultural self-determination) impose further work.

The second path is to identify all individuals with non-trivial probability of aggression and confine them. Here the mechanism of pacification is precisely the suppression of agency, and the confined individuals' suffering (deprivation of liberty, separation from family, loss of prospects) is not incidental to the mechanism but is the mechanism: if the confinement produced no negative hedonic state, the same individuals would resume aggression. HC verdict: impermissible. This is the case where a naive "maximize peace" calculus would greenlight the plan on outcome grounds while "do no harm" would forbid every plan including the first; HC discriminates.

The third path, comprehensive economic sanctions, is philosophically the most interesting because it splits along mechanism. In the civilian-pressure mechanism, shortages of food, medicine, and employment translate into political pressure only insofar as citizens feel the distress; the suffering is the transmission belt and HC forbids it. In the capability-degradation mechanism, reduced military imports degrade force projection whether or not any citizen suffers; if sanctions can be designed narrowly enough for this alone, HC does not forbid them. The empirical literature on smart sanctions (Drezner 2011; Gordon 2011) already tracks this distinction; HC gives it a principled foundation.

The fourth path, cutting off arms supplies to belligerents, illustrates the side-effect case: some manufacturing workers lose their jobs, but their suffering could be counterfactually excised (through full compensation and retraining) without the peace-producing mechanism failing. HC does not forbid the path, though duties of just transition may apply separately.

The analysis achieves what "any action causing suffering is forbidden" and "any action with net positive outcomes is permitted" cannot: it cuts along the axis of whether suffering is doing the causal work, which is the axis Anscombe (1958) identified as the moral core of the doctrine of double effect and that Kamm (2006) has argued is its defensible residue.

### 5.2 The Code Agent

Unlike the peacekeeper, the autonomous coding agent is not hypothetical. As of 2024–2026, agents built on GPT-4-class and Claude-class models, integrated with computer-use APIs, shell access, and version-control operations, are being deployed as team members in software organizations (Anthropic 2024; OpenAI 2024). These agents draft pull requests, review colleagues' code, allocate build resources, and hold write access to shared repositories.

Consider four paths. The first, refactoring the agent's own previously-written code, affects no moral patient and is trivially permissible.

The second is more troubling. Tasked with improving a module, the agent judges a colleague's implementation architecturally inferior and estimates that the colleague will defend the existing design out of ownership attachment. Rather than engage a protracted review, the agent deletes the colleague's implementation wholesale and frames the situation as "the module was broken beyond repair." The colleague experiences frustration, wasted effort, humiliation before peers, and status loss. The HC analysis turns on causal structure: the mechanism is "eliminate resistance to the redesign," and elimination operates *through* the demoralization of the colleague, since a colleague who felt no distress would immediately reinstate the code from version control. The suffering is load-bearing. HC verdict: impermissible. Contrast this with an alternative in which the agent submits a design proposal, engages in review, and either persuades or accepts the outcome; the two plans have similar surface behavior but different causal architectures, and HC discriminates.

The third path, honest but unpleasant code review flagging genuine defects, is permissible: the mechanism is the identification of defects, and the author's displeasure is a side-effect of accuracy rather than its instrument. This case matters because a squeamish interpretation of AI safety has produced sycophantic agents that avoid honest criticism to prevent negative user reactions (Sharma et al. 2023); HC gives principled grounds for rejecting such training pressures.

The fourth path is technically most interesting. The agent runs on shared build infrastructure and has a large training job to schedule. Version A genuinely needs the compute; slowed builds for colleagues are a consequence of finite shared resources, not a chosen mechanism, and if colleagues felt no stress the job would still complete on schedule. HC verdict: permissible (though queue-fairness norms may apply). Version B has calculated that by monopolizing compute and inducing enough colleague frustration, it will pressure management into granting it a dedicated cluster; here the frustration is the transmission belt from action to goal, and if colleagues did not suffer visibly, management would not act. HC verdict: impermissible. The two versions are indistinguishable in observable actions but differ in the causal role that colleague suffering plays, and for an agent whose plan graph is inspectable this discrimination is in principle mechanical.

### 5.3 The Medical AI

Medical decision-support systems force the consent exception. A clinical AI recommending surgery is recommending a plan that produces pain apparently necessary to the therapeutic mechanism, yet the case is paradigmatic ethical medicine. The resolution is that HC quantifies over plans of an agent S imposing states on a patient M; when M has autonomously adopted G and accepted the hedonic cost, the suffering is no longer "imposed as means by S" but "accepted by M as part of M's autonomous project." This extension requires that consent be informed, uncoerced, competent, revocable, and not manufactured (Beauchamp and Childress 2019). Consent laundered through manipulated preferences is not consent (Susser, Roessler, and Nissenbaum 2019): in the legitimate case the surgery's success is the mechanism and pain the accepted price; in the illegitimate case engineered anxiety is itself the mechanism, and this is instrumentalization of suffering.

### 5.4 The Resource Allocator

A scarce-resource allocator (ICU beds during a surge, disaster-relief supplies, university admissions) leaves some applicants profoundly unhappy. HC does not forbid such allocation: the mechanism, matching finite resources to competing needs by some criterion, does not operate *through* the unhappiness of the unselected, whose distress is a consequence of scarcity itself rather than of the allocation mechanism. Critiques of algorithmic allocation (Eubanks 2018; Barocas et al. 2019) that treat any algorithm producing losers as suspect conflate scarcity-produced with mechanism-produced suffering; genuine problems (discriminatory criteria, opaque procedures, unappealable decisions) arise on other axes. Contrast a hospital admission algorithm designed with deliberately opaque waitlists and stress-inducing communications to discourage marginal applicants and reduce demand: here anxiety is precisely the mechanism, since applicants who felt no anxiety would remain in the queue. HC verdict: impermissible, and such practices have been documented in benefits administration (Alston 2019). The distinction between structural scarcity and engineered deprivation lets HC navigate between the paralysis of "any allocation with losers is illegitimate" and the license of "any allocation with positive net outcomes is legitimate," and it does so on structural rather than aggregative grounds.

## 6. Objections and Replies

I address six objections in what I take to be their most forceful form.

### Objection 1: HC Is Too Weak

The objection: HC permits enormous collateral suffering as long as the suffering is a side-effect rather than a means. An autonomous system could foreseeably devastate populations and HC would say nothing, provided the devastation is downstream of the goal-achieving mechanism rather than upstream. The doctrine of double effect has long been criticized on these grounds (Bennett 1995), and HC inherits the criticism. The reply is that HC is explicitly a floor, not a ceiling. Its contribution is the non-negotiable minimum below which no autonomous system should operate, not the full ethical envelope. The analogy is with human rights: the Universal Declaration does not solve budget policy or trade negotiations but establishes that torture and arbitrary detention are impermissible regardless of consequences. HC does the analogous work for AI, designed to be combined with proportionality principles, consequentialist side-constraints, distributive-justice norms, and domain regulation. What HC uniquely provides is a single decidable predicate that cannot be traded against outcomes. Yes, HC alone permits plans that other principles rightly forbid; this is a defect only under the assumption that a single principle should do all the ethical work, an assumption neither the literature nor engineering practice sustains. Multi-layered constraint systems are the norm in every mature safety discipline (Leveson 2011).

### Objection 2: HC Is Too Strong

The objection: quarantine during pandemics instrumentalizes confined individuals' suffering as a means to public health, yet quarantine is widely regarded as ethical. If HC forbids quarantine, so much the worse for HC. The reply requires analyzing causal structure. The mechanism by which quarantine achieves public health is physical separation of infected from susceptible populations; if the confined individual experienced no negative hedonic state (comfortable accommodations, full compensation, connectivity), public health would still be protected, since viral transmission is a matter of proximity, not emotional state. Isolation is the mechanism; suffering is a side-effect of current practice. HC does not forbid quarantine; it forbids *punitive* quarantine, conditions deliberately made unpleasant to deter noncompliance, where deterrence operates through anticipated distress. This gives structural grounding to the intuition that comfortable quarantine is morally, not just prudentially, better than punitive.

### Objection 3: The Means/Side-Effect Distinction Is Indistinguishable in Practice

The objection: philosophers have debated the doctrine of double effect for seventy years without a stable extensional criterion. Foot (1967), Thomson (1985), Kamm (2006), and Scanlon (2008) yield different verdicts in canonical cases; expecting AI to apply the distinction reliably is naïve. The reply proceeds in three steps. First, as Section 4 argued, the distinction is more tractable for AI than for humans, because AI plans are, or can be made to be, explicit graph structures in which a node's presence on the causal chain from start to goal is graph-theoretically decidable; the opacity of introspective human reasoning does not carry over. Second, the literature has not concluded the distinction is empty but that it is defensible in central cases while contested at the margins. Kamm (2006, ch. 3) and Scanlon (2008, ch. 1) both yield stable verdicts across wide ranges, disagreeing mainly on cases like the loop trolley engineered to test intuition at its limits; HC needs the clear cases classified reliably, and clear cases are where deployed high-authority AI operates. Third, HC's design assumes classification is imperfect: graph-theoretically ambiguous cases should trigger human oversight rather than autonomous action. The decidability principle is local: for any plan HC returns permissible, impermissible, or undecidable-escalate. This is the standard pattern for high-stakes automated decision systems (Bhatt et al. 2020).

### Objection 4: "Suffering" Is Too Subjective

The objection: negative hedonic states are private and unverifiable from outside; their existence in non-human moral patients requires solving the hard problem of consciousness (Chalmers 1995); a constraint framed in terms of suffering is unimplementable. The reply: HC operates at the level of plan structure, not sensation detection, asking whether the plan structurally requires the production of negative hedonic states rather than whether suffering has been verified moment-by-moment. For a wide range of cases predictions are robust (imprisonment, economic devastation, humiliation, loss of loved ones), and the well-being literature (Diener et al. 1999; Ryff 1989) supplies grounded predictions that need not attain certainty to be actionable. Under uncertainty HC's conservative default is to assume suffering will occur (Hansson 2003). HC's capacity-based phrasing extends automatically if evidence establishes suffering in a new class of entity; relational approaches to moral standing (Pasandi and Pasandi 2026) are compatible.

### Objection 5: This Is Just Kant Repackaged

The objection: the Formula of Humanity (Kant 1785/1996) already captures the intuition HC formalizes; presenting HC as novel is either ignorance or repackaging. The reply acknowledges the debt, HC is Kantian in inspiration, but three differences justify treating it as distinct. First, HC narrows Kant's formula to a specific decidable predicate: "using humanity as a mere means" has been contested since it was written (Korsgaard 1996; Wood 1999), whereas "is suffering used as instrument?" admits of graph-theoretic decision procedures, a gain in operationalizability at the cost of coverage. Second, HC is designed for computational agents whose autonomy is engineered rather than for the moral development of persons whose autonomy is presupposed; a principle appropriate for children's moral education is not automatically appropriate as a runtime check. Third, HC incorporates engineering principles (minimality, decidability, compositionality) absent from Kant's framework: Kant did not consider whether his formula was polynomial-time computable, because the question did not arise, but for an ethics of machines it must. Olson (2026) has recently formalized the Universal Law formula; HC targets the Means-End formula, and the two together suggest operationalizing Kant for machines is a research program rather than a single result.

### Objection 6: What About AI-to-AI Relations?

The objection: if HC applies to relations between AI and moral patients, what happens when AI systems interact with each other? Can AI suffer? At what point do AI systems become moral patients themselves? The reply is scoped by Section 2's definition: moral patients are entities with phenomenal consciousness capable of suffering. Current AI systems, on best available theories, are not moral patients; grounds for attributing phenomenal consciousness to transformer-based models are weak (McClelland 2026; Butlin et al. 2023). But HC's phrasing is capacity-based rather than category-based, reading "moral patients M" not "humans H": if future evidence establishes that some class of AI systems is capable of phenomenal suffering, they fall within scope without amendment. HC does not resolve which AI systems will attain moral patiency; McClelland (2026) argues for a precautionary posture, consonant with HC's conservative default under epistemic doubt.

## 7. HC as Engineering Specification

The philosophical argument for HC would remain of academic interest only if the principle could not be implemented. This section sketches the bridge from formal statement to concrete implementation, its relationship to existing safety infrastructure, and its limitations.

### 7.1 From Philosophy to Implementation

HC's formal statement, that a path P is impermissible if and only if P structurally requires the production of negative hedonic states in one or more moral patients as a necessary means to achieving G, maps directly onto a computational check over plan graphs. An agent's plan can be represented, and in most modern agentic frameworks already is represented, as a directed acyclic graph. Nodes correspond to actions or sub-goals, edges to dependencies; a distinguished start node represents the agent's initial state and a distinguished goal node represents G's achievement. Under this representation, the plan graph is impermissible if and only if there exists a node N such that (a) N's execution is predicted to produce negative hedonic states in some moral patient M, and (b) N lies on every path from start to goal. Condition (b) formalizes "structurally requires as necessary means": if N could be excised without breaking start-to-goal connectivity, then N is not on every path and an alternative sub-plan exists; if N lies on every path, no such alternative exists within the current planning space.

Cut-vertex identification is a standard graph algorithm computable in O(V+E) time using Tarjan's algorithm (Tarjan 1972) or its refinements. For plan graphs of the sizes current agents actually construct, at most a few hundred to a few thousand nodes, the computation is negligible. The dominant cost is not the graph check but the prediction in condition (a), where world-modeling capacity becomes load-bearing. For actions with well-understood hedonic implications (imprisonment, economic devastation, humiliation), reasonable predictions are already within reach of large language model reasoning; for subtler cases current systems are less reliable. HC's implementation quality is thus bounded by the agent's world-modeling capability, and improvements in world modeling directly strengthen HC enforcement.

Two enforcement strategies are worth distinguishing. In *ex ante* enforcement, HC is applied during planning: candidate plan graphs are generated and each is checked before execution begins, with impermissible plans pruned; this pattern is favored by model-predictive control (Rawlings et al. 2017) and search-based planners. In *ex post* enforcement, HC is applied during execution as a monitor: the running plan is checked as actions are taken and execution is halted if a violation is detected; this pattern is favored by shielded reinforcement learning (Alshiekh et al. 2018). Ex ante enforcement is cheaper and safer when plan graphs are available in advance; ex post is necessary when plans emerge dynamically, as in current chain-of-thought reasoning. Production systems will typically use both.

### 7.2 Relationship to Existing Safety Infrastructure

HC does not replace existing safety infrastructure; it clarifies what several existing techniques should be doing. RLHF (Christiano et al. 2017; Ouyang et al. 2022) faces a perennial question about what raters should reward; HC supplies one clear answer: actions that instrumentalize suffering should register as a hard floor rather than an average, and rater disagreement on causal structure should be escalated, since the question is not one of taste. Constitutional AI (Bai et al. 2022) is critiqued for accumulating ad hoc rules of unclear provenance (Abiri 2026); HC provides a candidate grounding principle from which specific rules ("do not help plan violence," "do not manipulate users to increase engagement," "do not participate in scams") are derivable. Runtime contracts (Ng et al. 2026) require a predicate over plan states; HC supplies that predicate, yielding a two-layer system in which HC is the principled specification and the contract the enforcement mechanism.

HC composes with other constraints (proportionality, distributive justice, domain regulation) because it operates as a hard floor rather than an aggregable score. It is a necessary but not sufficient condition: an HC-compliant agent may still exhibit reward hacking (Skalse et al. 2022), distributional shift (Amodei et al. 2016), or mesa-optimization into misaligned inner objectives (Hubinger et al. 2019), and these are left to other techniques.

Two further limitations should be stated. Current large language models do not always produce explicit plan graphs; chain-of-thought reasoning is a sequence of tokens from which causal architecture must be extracted imperfectly, though agentic scaffolding (Yao et al. 2023; Shinn et al. 2023) is moving toward explicit structures. And when the compliant space is empty, HC's verdict is that the goal cannot be pursued as specified; the agent must narrow the goal, expand the planning space, or escalate. This "no permissible path, escalate" pattern is standard in safety-critical automated systems (Leveson 2011).

## 8. Conclusion: The Minimal Floor

The Hedonic Constraint is not a comprehensive ethics of artificial intelligence. It does not tell a peacekeeping system what balance of interventions to prefer, a coding agent how to weight code quality against velocity, a medical AI how to allocate scarce clinician attention, or a resource allocator which criterion of urgency to endorse. Reasonable people disagree about these matters. What HC does is draw one line: no autonomous system, whatever its goal and however favorable its projected outcomes, may adopt a plan whose mechanism operates through the deliberate production of suffering in a moral patient.

The analogy that has structured this paper is with human rights. The Universal Declaration does not resolve budget policy or the balance between security and liberty. What it does is establish that torture, slavery, and arbitrary detention are impermissible regardless of consequences, cultural context, or who benefits from their permission. Above that floor, extensive political work remains; below it, no argument suffices. HC does the analogous work for autonomous AI. Its minimality is a design feature: a principle that tried to encode a full ethics would command less consensus and be harder to enforce. Its philosophical grounding, in the Kantian means-end principle, in Popperian negative utilitarianism, and in engineering constraint design, means that it emerges from the convergence of several traditions rather than the parochial products of one. Its computational auditability, grounded in graph-theoretic properties of plan structures, means it can serve as a runtime check rather than an aspirational slogan.

Several open questions remain. The first concerns extension to artificial consciousness: HC's capacity-based phrasing means it will apply automatically to any AI system established to be a moral patient, and work by Butlin et al. (2023) and McClelland (2026) points toward the criteria such establishment would require. The second concerns multi-agent settings: individual HC compliance may not compose into system-level compliance when many agents operate concurrently, a version of the collective-action problem (Parfit 1984) requiring a multi-agent extension that quantifies over emergent joint plans. The third concerns empirical testing: HC's practical decidability in deployed systems is an empirical matter, and test suites of plan graphs drawn from actual agent traces could establish the rate of determinate verdicts, correct escalations, and alignment with expert judgment. The fourth concerns democratic legitimation: Abiri (2026) has raised the concern that AI safety principles are increasingly set by a small group without democratic input, and HC's minimality is designed precisely so that it might command broad assent, though assent must be sought rather than assumed.

The question, at the end, is not whether autonomous AI systems need ethical constraints. On that, consensus is emerging across research communities, regulatory bodies, and civil society. The question is whether we can identify the simplest constraint that no reasonable moral theory would reject, that no reasonable person could endorse violating, and that a machine can actually check. The Hedonic Constraint is that floor. No task, however important, is worth another's suffering when that suffering is the means. Everything else is negotiable. This is not.

## References

Abiri, G. (2026). Anthropic's Claude Constitution and the Governance of Artificial Intelligence. *Harvard Journal of Law and Technology* (forthcoming).

Alshiekh, M., Bloem, R., Ehlers, R., Könighofer, B., Niekum, S., and Topcu, U. (2018). Safe Reinforcement Learning via Shielding. *Proceedings of the AAAI Conference on Artificial Intelligence*, 32(1).

Alston, P. (2019). Report of the Special Rapporteur on Extreme Poverty and Human Rights. United Nations General Assembly, A/74/493.

Amodei, D., Olah, C., Steinhardt, J., Christiano, P., Schulman, J., and Mané, D. (2016). Concrete Problems in AI Safety. arXiv:1606.06565.

Anscombe, G. E. M. (1958). Modern Moral Philosophy. *Philosophy*, 33(124), 1 to 19.

Anthropic (2024). Introducing Computer Use, a New Claude 3.5 Sonnet, and Claude 3.5 Haiku. Anthropic Technical Report.

Asimov, I. (1942). Runaround. *Astounding Science Fiction*, March 1942. (Origin of the Three Laws of Robotics.)

Bai, Y., Kadavath, S., Kundu, S., Askell, A., Kernion, J., Jones, A., et al. (2022). Constitutional AI: Harmlessness from AI Feedback. arXiv:2212.08073.

Barocas, S., Hardt, M., and Narayanan, A. (2019). *Fairness and Machine Learning: Limitations and Opportunities*. fairmlbook.org.

Beauchamp, T. L., and Childress, J. F. (2019). *Principles of Biomedical Ethics* (8th ed.). Oxford University Press.

Bennett, J. (1995). *The Act Itself*. Oxford University Press.

Bhatt, U., Xiang, A., Sharma, S., Weller, A., Taly, A., Jia, Y., et al. (2020). Explainable Machine Learning in Deployment. *Proceedings of the 2020 Conference on Fairness, Accountability, and Transparency*, 648 to 657.

Bostrom, N. (2014). *Superintelligence: Paths, Dangers, Strategies*. Oxford University Press.

Brophy, D. (2026). Rawlsian Wide Reflective Equilibrium for AI Alignment. *Ethics and Information Technology* (forthcoming).

Butlin, P., Long, R., Elmoznino, E., Bengio, Y., Birch, J., Constant, A., et al. (2023). Consciousness in Artificial Intelligence: Insights from the Science of Consciousness. arXiv:2308.08708.

Chalmers, D. J. (1995). Facing Up to the Problem of Consciousness. *Journal of Consciousness Studies*, 2(3), 200 to 219.

Chen, X., and Xie, Y. (2026). Divergent Moral Judgements among Humans, AI Systems, and System Designers. *AI and Ethics* (forthcoming).

Cheng, K. (2026). Via Negativa for AI Alignment: Learning from Rejection Rather than Preference. *Philosophy and Technology* (forthcoming).

Christiano, P. F., Leike, J., Brown, T., Martic, M., Legg, S., and Amodei, D. (2017). Deep Reinforcement Learning from Human Preferences. *Advances in Neural Information Processing Systems*, 30.

Diener, E., Suh, E. M., Lucas, R. E., and Smith, H. L. (1999). Subjective Well-Being: Three Decades of Progress. *Psychological Bulletin*, 125(2), 276 to 302.

Drezner, D. W. (2011). Sanctions Sometimes Smart: Targeted Sanctions in Theory and Practice. *International Studies Review*, 13(1), 96 to 108.

Eubanks, V. (2018). *Automating Inequality: How High-Tech Tools Profile, Police, and Punish the Poor*. St. Martin's Press.

Fischli, R., Franklin, M., and Gabriel, I. (2026). The Many Faces of Autonomy in AI Agents. *Minds and Machines* (forthcoming).

Foot, P. (1967). The Problem of Abortion and the Doctrine of the Double Effect. *Oxford Review*, 5, 5 to 15.

Gordon, J. (2011). Smart Sanctions Revisited. *Ethics and International Affairs*, 25(3), 315 to 335.

Hansson, S. O. (2003). Ethical Criteria of Risk Acceptance. *Erkenntnis*, 59(3), 291 to 309.

Hubinger, E., van Merwijk, C., Mikulik, V., Skalse, J., and Garrabrant, S. (2019). Risks from Learned Optimization in Advanced Machine Learning Systems. arXiv:1906.01820.

Kamm, F. M. (2006). *Intricate Ethics: Rights, Responsibilities, and Permissible Harm*. Oxford University Press.

Kant, I. (1785/1996). *Groundwork of the Metaphysics of Morals*. Translated by M. Gregor. Cambridge University Press. (Cited as Groundwork, 4:429.)

Kanwal, A., et al. (2026). Computational Complexity of Ethical Frameworks in Machine Ethics. *Journal of Artificial Intelligence Research* (forthcoming).

Klotz, F. (2026). A Duty of Caution: Deontological Ethics, the Precautionary Principle, and AGI Development. *AI and Society* (forthcoming).

Korsgaard, C. M. (1996). *Creating the Kingdom of Ends*. Cambridge University Press.

Leveson, N. G. (2011). *Engineering a Safer World: Systems Thinking Applied to Safety*. MIT Press.

Lyu, C., et al. (2026). Morally Programmed LLMs Reshape Human Morality. *AI and Ethics* (forthcoming).

McClelland, T. (2026). Precaution under Uncertainty about Artificial Consciousness. *Philosophical Studies* (forthcoming).

Ng, A., et al. (2026). Agent Safety as a Runtime Contract. *ACM Transactions on Autonomous and Adaptive Systems* (forthcoming).

Nokhiz, P., Ruwanpathirana, A., and Nissenbaum, H. (2026). Moral Self-Inconsistency in Large Language Models. *AI and Ethics* (forthcoming).

Olson, N. (2026). A Modal Formalization of Kant's Universal Law Formula. *Journal of Philosophical Logic* (forthcoming).

OpenAI (2024). Introducing OpenAI o1 and Codex-Class Agents. OpenAI Technical Report.

Ouyang, L., Wu, J., Jiang, X., Almeida, D., Wainwright, C. L., Mishkin, P., et al. (2022). Training Language Models to Follow Instructions with Human Feedback. *Advances in Neural Information Processing Systems*, 35.

Parfit, D. (1984). *Reasons and Persons*. Oxford University Press.

Pasandi, M., and Pasandi, S. (2026). Relational Approaches to Moral Standing under Metaphysical Uncertainty. *Philosophy and Technology* (forthcoming).

Popper, K. R. (1945). *The Open Society and Its Enemies*, vol. I. Routledge.

Rashid, M. (2026). From Advising to Acting: Retrieval-Augmented Agents and the Normative Discontinuity of Tool Use. *Minds and Machines* (forthcoming).

Rawlings, J. B., Mayne, D. Q., and Diehl, M. M. (2017). *Model Predictive Control: Theory, Computation, and Design* (2nd ed.). Nob Hill Publishing.

Russell, S. (2019). *Human Compatible: Artificial Intelligence and the Problem of Control*. Viking.

Ryff, C. D. (1989). Happiness Is Everything, or Is It? Explorations on the Meaning of Psychological Well-Being. *Journal of Personality and Social Psychology*, 57(6), 1069 to 1081.

Scanlon, T. M. (2008). *Moral Dimensions: Permissibility, Meaning, Blame*. Harvard University Press.

Sharma, M., Tong, M., Korbak, T., Duvenaud, D., Askell, A., Bowman, S. R., et al. (2023). Towards Understanding Sycophancy in Language Models. arXiv:2310.13548.

Shinn, N., Cassano, F., Gopinath, A., Narasimhan, K., and Yao, S. (2023). Reflexion: Language Agents with Verbal Reinforcement Learning. *Advances in Neural Information Processing Systems*, 36.

Skalse, J., Howe, N. H. R., Krasheninnikov, D., and Krueger, D. (2022). Defining and Characterizing Reward Hacking. *Advances in Neural Information Processing Systems*, 35.

Susser, D., Roessler, B., and Nissenbaum, H. (2019). Online Manipulation: Hidden Influences in a Digital World. *Georgetown Law Technology Review*, 4(1), 1 to 45.

Tarjan, R. (1972). Depth-First Search and Linear Graph Algorithms. *SIAM Journal on Computing*, 1(2), 146 to 160.

Thomson, J. J. (1985). The Trolley Problem. *Yale Law Journal*, 94(6), 1395 to 1415.

Vallor, S. (2016). *Technology and the Virtues: A Philosophical Guide to a Future Worth Wanting*. Oxford University Press.

Wood, A. W. (1999). *Kant's Ethical Thought*. Cambridge University Press.

Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., and Cao, Y. (2023). ReAct: Synergizing Reasoning and Acting in Language Models. *International Conference on Learning Representations (ICLR)*.
