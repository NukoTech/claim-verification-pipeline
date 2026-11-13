---
name: claim-verification-pipeline
description: "Six-layer automated claim verification: corpus construction, entity and claim extraction, intra-document consistency, cross-source triangulation, external signal corroboration, hypothesis matrix. Domain-agnostic. Activate when evaluating technical claims, performing due diligence, assessing vendor claims, or verifying research findings. Triggers: is this claim true, verify this, due diligence, fact check, evaluate this technology."
---


# Claim Verification Pipeline

## The Verification Gap

The gap between surface-level factual accuracy and deeper methodological validity. A naive LLM 
would ingest a paper claiming "runtime quantum advantage" and confidently report that advantage 
has been achieved — simply trusting the abstract. Structured verification catches what naive 
summarization misses.

## The Six-Layer Pipeline

```
Layer 1: CORPUS CONSTRUCTION    → Build the evidence base
Layer 2: ENTITY & CLAIM EXTRACTION  → Decompose into structured triples
Layer 3: INTRA-DOCUMENT VERIFICATION  → Check document against itself
Layer 4: CROSS-SOURCE VERIFICATION   → Triangulate across sources
Layer 5: EXTERNAL SIGNAL CORROBORATION → Check commercial/financial context
Layer 6: HYPOTHESIS MATRIX           → Generate scored assessment
```

Each layer receives structured outputs from the prior layer and passes enriched results forward.

### Layer 1: Corpus Construction & Ingestion

**Goal**: Build a reliable, bias-aware evidence base.

1. Search across diverse source types (papers, patents, profiles, news)
2. Score each source for quality (citations, venue, affiliations, bias indicators)
3. Extract text, visual assets, metadata
4. Embed and store in searchable format

**Key principle**: Corpus is bias-aware — sources from commercially interested parties are 
flagged, not excluded.

### Layer 2: Entity & Claim Extraction

**Goal**: Decompose every assertion into structured, verifiable units.

**Claim Triple**: (Subject, Predicate, Object)
```
Example: (BF-DCQO, outperforms, SA by 3.5x)
Example: (Algorithm X, requires, GPU with 80GB VRAM)
Example: (Vendor Y, claims, 99.99% uptime)
```

**Provenance Classification** (5-tier hierarchy):
| Level | Type | Weight |
|-------|------|--------|
| 1 | Experimental Data | Highest |
| 2 | Simulation Result | High |
| 3 | Theoretical Estimate | Medium |
| 4 | Citation of Another Work | Low |
| 5 | Author Assertion (no evidence) | Lowest |

**Metric Normalization**: Convert all quantitative claims to standardized units. 
Flag definitional discrepancies (e.g., "runtime" measured differently by different parties).

### Layer 3: Intra-Document Verification

**Goal**: Does the document's OWN evidence support its OWN claims?

Three checks:
1. **Claim-Evidence Alignment**: For each claim triple, locate supporting evidence within the 
   SAME document. Classify as: Supports, Contradicts, or Neutral.
2. **Methodology-Result Coherence**: Does the experimental methodology logically support the 
   reported results? Check scope consistency, baseline fairness, reproducibility.
3. **Overclaim Detection**: Flag where conclusions exceed evidence:
   - Abstract claims broader than body text supports
   - Qualifiers dropped between methods and conclusions
   - Future projections presented as established results
   - Instance-specific results presented as general findings

**Output**: Document-level consistency score = proportion of claims supported by internal evidence.

**The Pattern to Catch**: Cautious methods sections ("best-performing instance," "can potentially") 
with assertive abstracts/conclusions ("achieving advantage," "industrial-scale"). This pattern 
(careful methods, bold framing) is a structural signal of strategic overclaiming.

### Layer 4: Cross-Source Verification

**Goal**: Do INDEPENDENT sources agree?

Three retrieval strategies:
1. **Citation traversal**: Rebuttals, follow-ups, foundational studies
2. **Semantic similarity**: Topically related works without citation links
3. **Entity-based graph traversal**: Documents sharing core entities

For matched claims across sources:
- **Citation Fidelity**: When Source A cites Source B, does Source B actually say what Source A claims?
- **Contradiction Root Cause**: When sources disagree, WHY? (methodology differences, 
  incompatible conditions, different benchmarks, cherry-picking vs averaging)

**Source Independence Assessment**:
- Author overlap → down-weight
- Institutional affiliation → down-weight
- Citation graph proximity → down-weight
- Internal inconsistency (from Layer 3) → down-weight

**The Self-Correction Signal**: Track the claimant's OWN publication trajectory. If they retreat 
from strong claims in later papers, that's stronger evidence than external critiques.

### Layer 5: External Signal Corroboration

**Goal**: What does the MONEY say?

- **Financial Profile**: SEC filings, funding, CapEx vs OpEx patterns
- **Conflict of Interest**: Author → corporate officer → commercial product links
- **Supply Chain Dependencies**: Hardware requirements, vendor lock-in, manufacturing chain
- **Publication-Product Timing**: Commercial launch → paper claiming advantage (suspicious)
- **Strategic Timeline**: Partnerships, acquisitions, funding rounds

Uses multi-hop reasoning over extracted entities to discover hidden relationships.

### Layer 6: Hypothesis Matrix

**Goal**: Produce a scored intelligence assessment.

For each claim, aggregate:
- Provenance level (Layer 2)
- Consistency verdict (Layer 3)
- Cross-source consensus (Layer 4)
- Entity-level signals (Layer 5)

Generate:
- Testable hypotheses with supporting evidence
- Adversarial counter-hypotheses
- Confidence levels (Low/Medium/High) based on semantic entropy
- Final labels: **Supported**, **Needs Review**, or **Likely Hallucination**
- Technology maturity assessment (TRL rating)
- Alpha signal detection (all layers converge positively?)

## Quick Application Protocol

For everyday use (not full research pipeline), apply the layers as mental checks:

1. **What exactly is being claimed?** (Layer 2 — decompose into triples)
2. **Does the document's own evidence support the claim?** (Layer 3)
3. **Do independent sources agree?** (Layer 4 — emphasis on INDEPENDENT)
4. **Who benefits from this claim being believed?** (Layer 5)
5. **What's the honest confidence level?** (Layer 6)

## Deployment Map

### Construction — Vendor Verification
- Equipment manufacturer performance claims vs independent testing
- Subcontractor capability claims vs past performance records
- Material specification claims vs third-party certification

### Federal Contracting — Technical Evaluation
- Technical proposal evaluation against past performance
- Capability claims vs evidence in technical volume
- Small business size/status verification
