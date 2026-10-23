# Hybrid Design Rationale

## Purpose

This document explains the rationale for the hybrid architecture derived from the comparative evaluation reported in:

Jean-Pierre Messerli. *Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns.*

The hybrid architecture is not a fourth evaluated implementation pattern. It is a design synthesis derived from the comparative evaluation of the FOLDER-, LINK-, and CLUSTER-based patterns.

The synthesis proposes distinct architectural responsibilities for the openEHR mechanisms based on the comparative design findings. This allocation is an architectural interpretation, not an empirically validated optimization or a demonstrated advantage over other combinations.

## Basis of the synthesis

All three evaluated patterns supported the eight clinician-centered functional requirements at design level when combined with the common information model and synthetic longitudinal medical record.

The architectural comparison nevertheless showed that the patterns distribute responsibilities differently:

-   FOLDER represents patient-level organization and navigation through the EHR Directory
-   LINK represents explicit RM-level relationships between LOCATABLE objects
-   CLUSTER represents governed relationship metadata within archetypes and templates

The synthesis follows a separation-of-concerns principle. This principle informs the proposal but was not itself tested through an integrated hybrid implementation.

It does not designate one of the three patterns as universally superior. Instead, it proposes a narrower role for each mechanism based on architectural characteristics identified in the comparative evaluation. The resulting allocation remains a design hypothesis.

## Synthesized architecture

| Architectural responsibility | Proposed mechanism | Rationale |
| --- | --- | --- |
| Longitudinal representation of a Health Problem | Episode-of-Care COMPOSITION | Provides the longitudinal identity and lifecycle of a distinct Health Problem in the adopted model. |
| Governed relationship semantics | Relationship CLUSTERs | Provides archetype- and template-governed structures for Care Encounter and Episode associations, relationship roles, cardinalities, and modeled classifications. |
| Patient-wide hierarchical navigation | FOLDER | Provides a separately maintained patient-level navigation and indexing structure over existing EHR content. |
| Selective explicit object-to-object relationships | LINK | Provides an RM-level mechanism where an explicit relationship between LOCATABLE objects is appropriate. |
| Clinical statements | Archetyped ENTRYs within clinical COMPOSITIONs | Preserves clinical statements in their source structures rather than duplicating them in Episode, navigation, or view-specific representations. |
| Derived linear lists and clinical views | Query and application layer | Derives separate Diagnosis and Problem Lists from Episode-of-Care COMPOSITIONs using `Classification = Diagnosis` or `Classification = Problem`, and constructs other views without duplicating authoritative content. |

## 1. Episode-of-Care COMPOSITION as the longitudinal Health Problem representation

In the synthesized design, the Episode-of-Care COMPOSITION represents the longitudinal identity and lifecycle of one distinct Health Problem.

It provides a stable longitudinal representation to which clinical information can be related across multiple Care Encounters.

The Episode-of-Care COMPOSITION is **not** intended to become a duplicate container for all clinical statements associated with the Health Problem. Clinical observations, evaluations, instructions, and other clinical statements remain in their source ENTRYs and COMPOSITIONs.

This separation allows the Episode to provide longitudinal continuity while preserving the provenance and native lifecycle of the source clinical information.

Two separate linear views can therefore be derived from the existing Episode-of-Care COMPOSITIONs: a Diagnosis List containing Episodes with `Classification = Diagnosis`, and a Problem List containing Episodes with `Classification = Problem`. Neither view requires a second authoritative copy of the Episode or its clinical information.

## 2. Relationship CLUSTERs for governed semantic associations

The comparative evaluation identified archetyped CLUSTERs as providing the strongest in-template semantic governance among the evaluated designs. This finding supports considering CLUSTERs for relationships requiring explicit modeled semantics, but does not establish that this allocation is optimal in production.

The synthesized architecture therefore uses relationship CLUSTERs for modeled association metadata such as:

-   Care Encounter reference
-   primary Episode-of-Care association
-   optional additional associated Episode-of-Care associations
-   Episode association role
-   Clinical Section classification
-   SOAP classification where applicable
-   other modeled relationship attributes required by a defined use case

The relevant repository artifacts are maintained in `local/`, including:

-   `openEHR-EHR-CLUSTER.eoc_relationships_entry.v0.adl`
-   `openEHR-EHR-CLUSTER.eoc_relationships_care_encounter.v0.adl`
-   `openEHR-EHR-CLUSTER.eoc_relationships_episode_of_care.v0.adl`

Their manuscript-specific mapping is documented in:

[`README.md`](../02-implementation-patterns/cluster/README.md)

This allocation reflects the finding that CLUSTER provided the strongest in-template semantic governance in the evaluated design. It should not be interpreted as a general claim that CLUSTER is superior for every kind of relationship.

## 3. FOLDER for patient-wide navigation and indexing

In the hybrid design, FOLDER serves patient-wide organization, navigation, and indexing.

FOLDER can provide alternative hierarchical navigation structures over existing EHR content without duplicating clinical statements.

Possible navigation structures include:

-   Care Encounter-oriented navigation
-   Episode-oriented navigation
-   Clinical Section-oriented navigation
-   other patient-level organizational structures where hierarchical navigation is useful

The representative artifact is:

[`folder-example.json`](../02-implementation-patterns/folder/folder-example.json)

In the hybrid architecture, FOLDER membership is not intended to carry the complete governed semantics of the Episode relationship. Those semantics are represented through the modeled relationship structures.

This separation allows the Directory to evolve as a navigation structure while clinical statements remain in their source COMPOSITIONs and governed relationship metadata remains within the modeled clinical structures.

## 4. LINK for selective explicit RM-level relationships

LINK remains useful where an explicit RM-level object-to-object relationship is appropriate.

The hybrid design retains LINK as a selective mechanism rather than using it as the primary representation for every Episode and Care Encounter relationship.

Representative examples are documented in:

-   [`care-encounter-links.json`](../02-implementation-patterns/link/care-encounter-links.json)
-   [`episode-of-care-links.json`](../02-implementation-patterns/link/episode-of-care-links.json)

Potential use depends on the relationship that an implementation needs to make explicit and on agreed conventions for meaning, type, direction, target, and granularity.

Where information required by a workflow resides in the LINK target, target resolution remains necessary.

## 5. Clinical ENTRYs remain the source of clinical statements

The hybrid architecture separates relationship organization from clinical content ownership.

Clinical statements remain represented by the appropriate archetyped ENTRYs within clinical COMPOSITIONs.

The Episode-of-Care representation, relationship CLUSTERs, FOLDER navigation structures, and LINK relationships should not create competing authoritative copies of those clinical statements.

This distinction matters because the same clinical statement may participate in several perspectives simultaneously. A statement can belong to a Care Encounter, relate primarily to one Health Problem, also be relevant to another Health Problem, belong to a Clinical Section, and participate in a SOAP-oriented view.

These perspectives are represented as relationships, classifications, or derived views rather than as duplicated clinical statements.

A complete SOAP progress note is treated as one clinical documentation unit, although the adopted SOAP template represents Subjective, Objective, Assessment, and Plan using four technical `OBSERVATION.progress_note.v1` ENTRYs under `SECTION.soap.v0`.
Its Episode-of-Care assignment should therefore remain consistent across those four ENTRYs as a clinical modeling requirement. The study did not establish automatic server-side enforcement of this cross-ENTRY invariant. Technical ENTRY granularity must not be mistaken for four independently assignable clinical notes.

## 6. Derived views remain projections

The eight clinician-centered requirements evaluated in the study describe different ways of organizing or viewing the same longitudinal clinical record.

The hybrid design therefore treats views such as the following as projections over the underlying information:

-   chronological Care Encounter view
-   Episode-oriented view for a selected Health Problem
-   Clinical Section view
-   combined Clinical Section and Care Encounter or Episode view
-   linear Diagnosis List (`Classification = Diagnosis`)
-   linear Problem List (`Classification = Problem`)
-   SOAP-oriented view
-   section-oriented dashboard

The hierarchical Diagnosis and Problem List is distinct from these derived linear views. It is represented by a separate COMPOSITION that persists the clinician-curated hierarchy and explicit references to existing Episode-of-Care COMPOSITIONs, without duplicating their clinical content. This clinically curated hierarchy is also distinct from the patient-wide FOLDER Directory used for navigation and indexing. Consequently, it is not merely an automatically generated projection; its curated structure is itself persisted.

The query and application layer is responsible for constructing these views from the authoritative source information and relationship structures.

## Separation of concerns

The synthesized architecture assigns distinct responsibilities to the following openEHR structures and application components:

**Episode-of-Care COMPOSITION**
Longitudinal identity and lifecycle of a Health Problem

**Relationship CLUSTERs**
Governed relationship semantics and classifications

**FOLDER**
Patient-wide hierarchical navigation and indexing

**LINK**
Selective explicit object relationships using the openEHR Reference Model

**Clinical ENTRYs and COMPOSITIONs**
Authoritative clinical content and its provenance

**Hierarchical Diagnosis and Problem List COMPOSITION**
Persisted clinician-curated hierarchy referencing Episode-of-Care COMPOSITIONs

**Query and application layer**
Derived linear Diagnosis and Problem Lists and other clinical views

The objective is not to maximize the number of openEHR mechanisms used, but to propose a coherent division of responsibilities informed by the comparative evaluation. The relative suitability of this allocation requires empirical assessment.

## Relationship to the comparative evaluation

The hybrid architecture is derived from the findings documented in:

-   `architectural-evidence-matrix.csv`
-   [`functional-requirements.md`](../04-functional-evaluation/functional-requirements.md)
-   [`functional-traceability.csv`](../04-functional-evaluation/functional-traceability.csv)
-   the FOLDER, LINK, and CLUSTER artifacts under `../02-implementation-patterns/`

The functional evaluation established that all three patterns could support the eight requirements at design level.

The architectural evaluation then identified differences in:

-   location of relationship representation
-   semantic governance
-   relationship granularity
-   support for multiple Episode associations
-   patient-wide navigation
-   query and retrieval workflow
-   versioning and provenance
-   implementation responsibility
-   cross-system dependencies
-   principal architectural strengths and trade-offs

The hybrid architecture synthesizes these architectural differences into a proposed allocation of responsibilities. The comparative evaluation supports the identified design trade-offs, while the specific combination and division of responsibilities constitute an interpretive design recommendation. No integrated hybrid prototype, head-to-head comparison of hybrid allocations, or optimization analysis was performed.

## Evidence status

The hybrid architecture is a testable design hypothesis.

It was derived from the comparative design evaluation but was not implemented and evaluated as an integrated fourth pattern. Its constituent mechanisms were examined separately, which does not establish their combined behavior or integration costs.

Accordingly, the study does not claim that the hybrid architecture has demonstrated:

-   superior runtime performance
-   superior usability
-   reduced implementation cost
-   production-scale scalability
-   clinical outcome benefits
-   multi-vendor interoperability
-   cross-repository reference resolution
-   superiority over alternative hybrid allocations

These questions require subsequent implementation and empirical evaluation.

## Intended future evaluation

A subsequent implementation study could evaluate the hybrid architecture across one or more openEHR platforms and test:

-   conformance of shared archetypes and templates
-   persistence and retrieval of the relationship structures
-   reference resolution across relevant objects and repositories
-   behavior of the patient-level Directory
-   versioning behavior under longitudinal updates
-   query portability
-   multi-vendor interpretation of relationship semantics
-   runtime characteristics under representative workloads
-   clinician usability of derived Episode-oriented views

Such work would move the evidence from comparative design evaluation toward empirical implementation and interoperability testing.
