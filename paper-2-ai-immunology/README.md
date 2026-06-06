# Paper 2: AI-Assisted Antibody Discovery

**Working Title**: AI as Immune System Accelerator: Computational Traversal of the Antibody Repertoire

**Status**: Research phase — requires significant repositioning due to field saturation

---

## Core Idea

The human immune system finds antibodies against pathogens through T-cell/B-cell interaction, V(D)J recombination, and affinity maturation in germinal centers. This process typically takes 1-4 weeks. Could AI traverse the antibody repertoire computationally to identify matching antibodies faster than the biological process?

---

## Reality Check

**This idea in its general form is not novel.** The entire field of AI-driven antibody discovery (AbCellera, Absci, Nabla Bio, Baker Lab, Chai Discovery, etc.) already does exactly this. Key existing work:

- **CloneBO** (arXiv 2412.07763) — literally "teaches a model how the immune system optimizes antibodies"
- **KA-Search** — searches 2.4 billion antibodies in 30 minutes
- **RFAntibody** (Nature 2025) — de novo antibody design validated by cryo-EM
- **tFold** (Nature Communications 2025) — nM-affinity mAbs designed computationally
- **Origin-1** (Absci 2026) — zero-prior epitope targeting

---

## Where Novelty Might Exist

1. **Perspective paper**: "What current AI antibody methods miss about germinal center biology" — incorporating stochasticity, Tfh dynamics, affinity ceilings
2. **Biological principle gap**: Most AI models ignore the "imperfect cell sorter" physics of GCs
3. **New inductive bias**: Incorporating the affinity-fitness response function from eLife 2026 into generative models
4. **Speed/scale**: Algorithmic improvements to repertoire search beyond KA-Search/XTNeighbor

---

## Key Papers to Read

### Foundational Reviews
- "AI-driven computational methods for antibody design and optimization" — PMC12279266
- "Revolutionizing oncology: AI for antibody design" — Biomarker Research 2025
- "AI Developments for T and B Cell Receptor Modeling" — arXiv 2601.17138

### Closest to Original Idea
- **CloneBO** (arXiv 2412.07763) — Bayesian optimization informed by immune system evolution
- **CoSiNE** (arXiv 2602.18982) — neural simulation of affinity maturation
- "Replaying germinal center evolution" — PMC12258878
- "Computing inducibility of bnAbs under context-dependent AM" — PMC12685565

### Tools & Benchmarks
- immuneML (Nature Machine Intelligence 2021)
- SAbDab (~9,000 antibody-antigen complexes)
- OAS (Observed Antibody Space)
- ProteinGym benchmarks

---

## Target Journals

| Journal | IF | Best For |
|---------|-----|----------|
| Briefings in Bioinformatics | ~9 | Review/method paper |
| Frontiers in Immunology (computational) | ~5.5 | Lowest barrier |
| PLOS Computational Biology | ~4.5 | Interdisciplinary |
| Artificial Life (MIT Press) | — | Bio-inspired AI |
| Nature Machine Intelligence | ~25 | Only with major breakthrough |

---

## Requirements for a Credible Paper

### Format A: Review/Perspective (most realistic without lab)
- ~150+ references
- Unique synthesis framework or new angle
- Risk: 5+ high-quality reviews published 2024-2026 already

### Format B: Computational simulation
- Novel algorithm/architecture
- Benchmark against RFAntibody, AlphaFold3, etc. on SAbDab/OAS
- Open-source code mandatory

### Format C: Computational + experimental (gold standard)
- All of Format B + wet-lab validation
- Cost: $50K-$500K, requires biology collaborator
- Target: Nature/Nature Biotechnology

---

## Recommendation

This paper requires the most additional work and domain expertise. Consider:
1. Finding an immunology co-author
2. Narrowing to a specific sub-question
3. Prioritizing Papers 1 and 3 first, returning to this with more preparation

---

## The Real Bottleneck (Not Search Speed)

The actual bottleneck in antibody discovery is NOT computational search time. It's:
- **Improbable mutations**: Critical mutations have near-zero probability under AID's biases
- **Data scarcity**: Only ~9,000 antibody-antigen structures available
- **Experimental validation**: Computational predictions still require wet-lab confirmation
