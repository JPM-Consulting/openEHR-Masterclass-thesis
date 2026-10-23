# Publications

This directory contains the principal scholarly outputs of the research on episode-oriented medical records and their representation in openEHR.

The publications reflect successive stages of the research. Although closely related, they are distinct outputs rather than successive versions of a single publication.

## Publication pathway

```text
Masterclass Thesis (2025)
        ↓
EHRCON26 Conference Abstract (2026)
        ↓
Frontiers Full Manuscript (2026)
```

The 2025 Masterclass thesis established the conceptual information model and its initial representation in openEHR. The accepted EHRCON26 abstract presented the work in a focused conference format. The Frontiers manuscript extends the research through a comparative design-level evaluation of three openEHR implementation patterns for representing Episode-of-Care relationships.

## Directory structure

```text
publications/
├── README.md
│
├── masterclass-thesis/
│   └── Messerli_2025_Masterclass_Thesis.pdf
│
├── ehrcon26/
│   └── Messerli_2026_EHRCON26_Abstract.pdf
│
└── frontiers/
    ├── README.md
    └── [supporting figures]
```

## Masterclass thesis

**Jean-Pierre Messerli. *Data Model of the Episode-Oriented Medical Record according to Solon in openEHR.* openEHR Masterclass Thesis, 2025.**

Location:

`masterclass-thesis/Messerli_2025_Masterclass_Thesis.pdf`

The thesis documents the original research, including its conceptual foundations, development of the episode-oriented information model, openEHR modeling artifacts, implementation considerations, and initial evaluation.

It remains the historical and methodological foundation of the subsequent work. The later comparative study refines the terminology, evaluation framework, implementation details, and interpretation of the findings.

## EHRCON26 conference abstract

**Jean-Pierre Messerli. *Modelling the Episode-Oriented Medical Record according to Solon in openEHR: Patterns for Longitudinal, Problem- and Episode-Centred Care.* EHRCON26, Amsterdam, 2026.**

Location:

`ehrcon26/Messerli_2026_EHRCON26_Abstract.pdf`

The accepted EHRCON26 abstract documents the conference-stage development of the research, connecting the original Masterclass thesis with the subsequent full manuscript.

It is retained as a distinct conference contribution, not as an earlier version of the Frontiers manuscript.

## Frontiers manuscript

**Jean-Pierre Messerli. *Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns.* 2026.**

Publication status and future article reference:

[`frontiers/README.md`](frontiers/README.md)

The manuscript is not included in this public repository during preparation, submission, or peer review.

The manuscript presents a structured, design-level comparison of three implementation patterns:

1. FOLDER-based organization
2. LINK-based relationships
3. CLUSTER-based relationship structures

The comparison distinguishes functional design adequacy from architectural characteristics. It uses a shared conceptual information model, a synthetic longitudinal patient record, and eight clinician-centered functional requirements. A scoped technical proof of concept provides separately documented implementation evidence.

The manuscript-specific evidence package is located at:

`../reproducibility/`

The manuscript and its reproducibility package provide the current framework for interpreting the comparative study. Where terminology, evaluation scope, implementation details, or conclusions differ from the earlier thesis or conference abstract, the current materials take precedence for this study.

## Relationship to the reproducibility package

The `publications/` directory contains scholarly outputs. The supporting evidence and openEHR modeling artifacts are maintained separately to distinguish publications from their underlying research materials.

The manuscript-specific reproducibility materials are located at:

`../reproducibility/`

The openEHR archetypes and templates are located at:

`../local/`

The three directories serve different purposes:

- publications: scholarly outputs
- local: openEHR archetype and template artifacts
- reproducibility: manuscript-specific evidence, traceability, evaluations, and retrieval examples

## Correction note on dataset size

The original openEHR Masterclass thesis and the EHRCON26 conference abstract report 132 entries. A subsequent reproducibility audit of the tabular source dataset confirmed **121 Medical Record Entries**. The earlier count included 11 blank rows used to visually separate Care Encounters. These separator rows are not clinical Medical Record Entries.

The historical publications remain unchanged. The current Frontiers manuscript and its reproducibility package consistently use the corrected count of **121 Medical Record Entries**.

## Versioning

Publication files should retain stable filenames. Git commits, tags, and repository releases should record version history rather than working-version suffixes in filenames.

The Frontiers manuscript is not distributed through this repository. After publication, the repository documentation should be updated with the definitive bibliographic details and persistent identifier. The `frontiers/README.md` serves as a stable entry point to the published article.

## Citation

Each publication should be cited according to its bibliographic status.

The repository-level `../CITATION.cff` provides citation metadata for the repository as a whole. Once the full article is published, its final citation and DOI can also be recorded as the preferred citation for the corresponding research output.

## Licensing

Each publication is subject to the license or publication terms applicable to that document. Inclusion in this repository does not automatically extend the repository-level license to individual publications.

See:

`../LICENSE.md`
