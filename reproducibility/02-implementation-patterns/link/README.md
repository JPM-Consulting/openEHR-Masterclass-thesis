# LINK-based implementation pattern

## Purpose

This directory provides representative artifacts for the LINK-based implementation pattern examined in:

**Jean-Pierre Messerli. *Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns.***

The examples build on the Reference Model (RM) LINK work documented in the Masterclass thesis and reflect the relationship design evaluated in the comparative manuscript.

## Artifacts

-   `care-encounter-links.json`: alternative LINK directions between a Care Encounter COMPOSITION and a clinical COMPOSITION
-   `episode-of-care-links.json`: LINK relationships between clinical ENTRYs and Episode-of-Care COMPOSITIONs, including primary and associated Episode relationships

Both files are **annotated documentation artifacts**. The objects under each `link` property represent RM LINK structures. The surrounding JSON wrapper identifies source and target roles to make relationship direction explicit. The wrapper is not an openEHR RM serialization suitable for direct submission to an EHR REST endpoint.

## Relationship to the original thesis

Appendix C of the Masterclass thesis documented RM-level LINK examples using `DV_EHR_URI` targets for:

1.  a COMPOSITION container or HEAD
2.  a specific COMPOSITION version
3.  an ENTRY path within a COMPOSITION

These examples provide the technical foundation for the LINK pattern.

The manuscript-specific artifacts retain the RM mechanism while focusing on the two relationship categories evaluated in the comparative study:

-   Care Encounter ↔ clinical COMPOSITION
-   clinical ENTRY ↔ Episode of Care

Labels used in the thesis, including `primary association to episode`, `episode_of_care`, `supports episode diagnosis`, and `diagnosis`, are not presented as standardized LINK semantics. The current artifacts distinguish relationship meaning from the manuscript-specific conventions expressed through `LINK.type`.

## Supporting technical notes

`link-technical-notes.pdf` records representative RM-level LINK examples explored during the thesis and associated proof-of-concept work. It illustrates `DV_EHR_URI` targets for a COMPOSITION container or HEAD, a specific COMPOSITION version, and an ENTRY path within a COMPOSITION. It also includes a minimal COMPOSITION skeleton containing a LINK.

The relationship labels in this document, including `primary association to episode`, `episode_of_care`, `supports episode diagnosis`, and `diagnosis`, are exploratory implementation examples rather than standardized openEHR LINK semantics. For the evaluated LINK design, the manuscript-specific JSON artifacts supersede these earlier examples and distinguish standardized relationship meanings, where applicable, from manuscript-specific conventions in `LINK.type`.

This document provides supporting evidence of the LINK pattern’s development and technical exploration. It does not establish a complete or production-validated implementation.

## openEHR Reference Model basis

`LINK` is inherited through `LOCATABLE` and contains three mandatory attributes:

-   `meaning: DV_TEXT`
-   `type: DV_TEXT`
-   `target: DV_EHR_URI`

`meaning` describes the relationship from the source object to the target object.

`type` provides a clinical or domain-level classification of the relationship.

`target` identifies the logical target of the relationship.

Because a LINK belongs to its owning LOCATABLE, changes to the LINK follow the version lifecycle of the version-controlled object containing that LOCATABLE.

## Care Encounter relationship

`care-encounter-links.json` illustrates the two alternative relationship directions considered in the manuscript:

### A. Care Encounter COMPOSITION → clinical COMPOSITION

The Care Encounter COMPOSITION owns a LINK targeting a clinical COMPOSITION generated in that Care Encounter.

### B. Clinical COMPOSITION → Care Encounter COMPOSITION

The clinical COMPOSITION owns a reciprocal-direction LINK targeting the corresponding Care Encounter COMPOSITION.

The two directions are **implementation alternatives**. The evaluated design does not require simultaneous persistence of both.

The `type` values are manuscript-specific implementation conventions, not standardized openEHR terminology.

## Episode-of-Care relationship

`episode-of-care-links.json` represents Episode-of-Care associations at ENTRY level, allowing different ENTRYs within one clinical COMPOSITION to relate to different Health Problems.

### A1. Clinical ENTRY → primary Episode of Care

The clinical ENTRY owns a LINK to its primary Episode-of-Care COMPOSITION.

### A2. Clinical ENTRY → associated Episode of Care

The same clinical ENTRY may own an additional LINK to another clinically relevant Episode-of-Care COMPOSITION.

The `type` values:

-   `episode-of-care-primary`
-   `episode-of-care-associated`

are explicit **design conventions of the evaluated implementation pattern**, not standardized openEHR LINK type codes.

### B. Episode of Care → clinical ENTRY

In the reverse direction, the Episode-of-Care COMPOSITION owns a LINK whose `DV_EHR_URI` targets an ENTRY within the source clinical COMPOSITION.

As with Care Encounter relationships, these directions are alternatives in the evaluated design. Reciprocal persistence is not required.

## Relationship meaning

The examples use relationship wording consistent with the final manuscript figures.

For the Care Encounter relationship, the examples use the directional meanings:

-   `documents`
-   `documented by`

For Episode association, the examples use:

-   `is related to the same care plan, act or episode`

These values convey the semantic direction of the representative relationships. The distinction between primary and associated Episodes is not encoded by `meaning` alone. It is expressed through the documented `type` convention.

## Synthetic identifiers

All EHR, COMPOSITION, and ENTRY identifiers in the examples are synthetic.

They make source-to-target relationships explicit and contain no real patient information.

## Relationship to the functional evaluation

The LINK artifacts provide representative design evidence for the LINK column of:

`../../04-functional-evaluation/functional-traceability.csv`

In particular, they illustrate mechanisms for:

-   chronological association with Care Encounter context
-   Episode-oriented retrieval across Care Encounters
-   association of an ENTRY with one primary and optional additional Episodes
-   preservation of source clinical content without Episode-specific duplication

The representative LINK artifacts focus on relationships between clinical content, Care Encounters, and Episodes of Care. Relationships involving Clinical Sections and SOAP documentation are outside the scope of these examples.

## Retrieval implications

A LINK does not ensure that all information needed for a clinical view is available within its source object.

When relevant information resides in the target object, the application must resolve the `DV_EHR_URI` target. Retrieval may therefore require relationship traversal and explicit target resolution.

The artifacts document how relationships are represented. They do not demonstrate that every LINK-based retrieval can be expressed in a single portable AQL query.

## Evidence boundary

At design level, these artifacts support the following claims:

-   LINK can represent explicit relationships between LOCATABLE openEHR objects
-   Care Encounter and clinical COMPOSITION relationships can be represented in alternative directions
-   Episode associations can be represented at clinical ENTRY level
-   one ENTRY can carry a primary Episode relationship and additional associated Episode relationships
-   `DV_EHR_URI` can identify the target object or a contained archetyped structure
-   clinical content need not be duplicated in order to establish the relationship

These artifacts do **not** establish:

-   a complete production implementation
-   persistence of reciprocal links in both directions
-   runtime or query performance
-   automatic referential-integrity enforcement
-   cross-repository target resolution
-   clinical usability
-   multi-vendor interoperability
-   superiority of LINK over FOLDER or CLUSTER

## Traceability

These artifacts should be read alongside:

-   `../../04-functional-evaluation/functional-requirements.md`
-   `../../04-functional-evaluation/functional-traceability.csv`
-   the architectural evidence matrix in `../../05-architectural-evaluation/`

The manuscript evaluates LINK as one of three openEHR-native approaches to representing relationships. Its distinguishing feature is the use of explicit RM-level relationships, supplemented by implementation conventions governing type, direction, target selection, and granularity.
