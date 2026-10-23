# Conceptual Model

This directory documents the conceptual foundation shared by all three implementation patterns examined in the comparative study:

**Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns**

The two figures establish a common information model for comparing the FOLDER-, LINK-, and CLUSTER-based implementation patterns.

## Contents

``` text
01-conceptual-model/
├── README.md
├── figure-1-conceptual-model.pdf
└── figure-2-openehr-mapping.pdf
```

## Figure 1: Conceptual model

`figure-1-conceptual-model.pdf`

Figure 1 presents a technology-independent conceptual model of the episode-oriented medical record.

The model distinguishes complementary dimensions and constructs of the longitudinal record:

-   **Care Encounter (Contact)**: a discrete care event or interaction in which clinical information is generated or documented
-   **Episode of Care (Health Problem)**: the longitudinal representation of one distinct Health Problem across one or more Care Encounters
-   **Administrative Encounter**: an organizational or service period that may encompass multiple Care Encounters
-   **Clinical Section**: a semantic classification of clinical information independent of its chronological or problem-oriented organization
-   **Medical Record Entry**: an individual clinical statement or documented clinical fact
-   **Partial Contact**: the conceptual part of a Care Encounter attributable to a particular Episode of Care

A Partial Contact is a conceptual relationship construct. It does not require a separately persisted object.

The Diagnosis and Problem List is modeled separately from the underlying longitudinal clinical record. It can provide a clinician-curated organization of diagnoses and problems without duplicating the associated clinical information.

## Figure 2: Mapping to openEHR

`figure-2-openehr-mapping.pdf`

Figure 2 maps the conceptual model to openEHR constructs without prescribing any of the three relationship implementation patterns evaluated in the study.

In this mapping:

-   Care Encounters are represented through dedicated openEHR COMPOSITIONs
-   an Episode of Care is represented through a longitudinal Episode-of-Care COMPOSITION associated with one distinct Health Problem
-   clinical statements remain represented by archetyped ENTRYs within clinical COMPOSITIONs
-   Administrative Encounters remain conceptually distinct from Care Encounters
-   relationships between Care Encounters, Episodes of Care, and clinical information are shown generically rather than prescribing FOLDER, LINK, or CLUSTER as the implementation mechanism

The Episode-of-Care COMPOSITION represents the longitudinal identity and lifecycle of an Episode of Care. It does not duplicate the clinical content associated with that episode.

## Pattern independence

Figures 1 and 2 establish a common conceptual baseline without favoring any implementation pattern.

The three alternative relationship representations are documented separately under:

``` text
../02-implementation-patterns/
├── folder/
├── link/
└── cluster/
```

This separation supports a controlled architectural comparison. The conceptual requirements remain constant, while the mechanism used to represent relationships varies.

## Role in the evaluation

The conceptual model provides a common semantic basis for:

-   the synthetic longitudinal patient record
-   the eight clinician-centered functional requirements
-   the FOLDER-, LINK-, and CLUSTER-based implementation patterns
-   the comparative architectural evaluation
-   the subsequent hybrid design rationale

The model thus connects the clinical concept of episode-oriented documentation with its alternative representations in openEHR.

## Evidence boundary

The figures are **design artifacts** that specify the conceptual model and its mapping to openEHR.

They do not by themselves demonstrate:

-   production deployment
-   runtime performance
-   usability or clinical outcomes
-   multi-vendor interoperability
-   superiority of one implementation pattern

The FOLDER, LINK, and CLUSTER patterns are evaluated separately at the design level.

## Manuscript mapping

These artifacts correspond to the conceptual modeling and openEHR mapping described in the manuscript’s Methods section and illustrated in Figures 1 and 2.

Detailed traceability between the manuscript and repository artifacts is documented in:

`../07-manuscript-mapping/manuscript-artifact-mapping.md`
