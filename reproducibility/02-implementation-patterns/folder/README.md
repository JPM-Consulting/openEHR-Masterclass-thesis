# FOLDER-based implementation pattern

## Purpose

This directory provides a representative artifact for the FOLDER-based implementation pattern examined in:

**Jean-Pierre Messerli. *Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns.***

The example builds on the FOLDER design developed in the Masterclass thesis. It has been simplified to reflect the scope of the manuscript-specific evaluation.

## Artifact

`folder-example.json`

The file illustrates an openEHR FOLDER hierarchy with three parallel patient-level navigation perspectives:

-   **Care Encounters**
-   **Episodes of Care**
-   **Clinical Sections**

The example is deliberately limited in scope. It illustrates the structural mechanism considered in the evaluation rather than reproducing the complete synthetic patient record of 121 Medical Record Entries.

## What the example demonstrates

The example illustrates four properties relevant to the comparative evaluation.

### 1. Patient-level hierarchical organization

The FOLDER hierarchy provides a patient-level navigation and indexing structure maintained independently of the referenced EHR objects.

Its three top-level branches offer alternative organizational perspectives on the same longitudinal record.

### 2. References rather than copied clinical content

The `items` attribute contains `OBJECT_REF` instances identifying existing `VERSIONED_COMPOSITION` objects.

The FOLDER structure references existing clinical content without copying it.

### 3. Multiple organizational perspectives without duplication

The same referenced clinical COMPOSITION may occur in more than one FOLDER.

For example, the synthetic clinical COMPOSITION identified as:

`aaaaaaaa-aaaa-4aaa-8aaa-aaaaaaaaaaaa`

is referenced under:

-   `Care Encounters / Care Encounter 001`
-   `Episodes of Care / Episode 001`
-   `Clinical Sections / Diagnostics`

This deliberate reuse allows the FOLDER hierarchy to index the same source object in multiple navigation structures without duplicating clinical content.

### 4. Separation of chronological, longitudinal, and semantic organization

The example keeps three dimensions distinct:

-   Care Encounter organization represents the chronological care-event perspective
-   Episode-of-Care organization represents the longitudinal Health Problem perspective
-   Clinical Section organization represents an additional semantic classification perspective

These distinctions reflect the multidimensional information model used in the study.

## Referenced objects

All identifiers in `folder-example.json` are synthetic and serve only to illustrate the relationship structure.

The example contains references representing:

-   two Care Encounter COMPOSITIONs
-   two Episode-of-Care COMPOSITIONs
-   three clinical COMPOSITIONs

Clinical COMPOSITION references recur across branches to illustrate alternative navigation paths to the same source information.

The identifiers do not originate from a real EHR and contain no patient information.

## Relationship to the synthetic evaluation dataset

The complete functional evaluation uses:

`../../03-synthetic-dataset/synthetic-patient-medical-record.xlsx`

The FOLDER example is a simplified representation of the mechanism considered in the functional design evaluation.

It is **not** a serialization of the complete synthetic dataset comprising 121 Medical Record Entries.

Accordingly, the artifact supports inspection of the hierarchy and COMPOSITION-level indexing, but does not illustrate finer-grained ENTRY- or SECTION-level references. It should not be interpreted as evidence that a complete FOLDER hierarchy representing 121 Medical Record Entries was persisted and executed on a production openEHR platform.

## Relationship to the original thesis artifacts

The underlying Masterclass thesis used generic FOLDER examples to explore patient-level organization, FOLDER metadata, references to versioned COMPOSITIONs, and alternative navigation structures.

For the manuscript-specific reproducibility package, the example retains only the elements relevant to the comparative evaluation.

### Scope of the illustrative example

This JSON artifact illustrates the hierarchical organization of the FOLDER pattern using `OBJECT_REF` references to existing versioned COMPOSITIONs. The same COMPOSITION can be referenced from multiple FOLDERs without duplicating its clinical content.

For simplicity, the example does not include `DV_EHR_URI` references to individual ENTRYs or SECTIONs. Such finer-grained references are part of the conceptual design illustrated in Figure 3 and were investigated in the Basic FOLDER proof of concept (T1). The example thus provides a simplified structural view rather than a complete implementation of the FOLDER pattern's relationship mechanisms.

Optional governance metadata from earlier generic examples is omitted to keep the focus on hierarchy and indexing.

## Supporting technical notes

`folder-technical-notes.pdf` documents an earlier generic FOLDER structure explored during the design work, including the use of FOLDER `details`, references to versioned EHR content, and `DV_EHR_URI` deep-link examples.

The document uses `openEHR-EHR-FOLDER.generic.v1` as the generic FOLDER archetype node identifier used by EHRbase. This identifier should be interpreted as an implementation convention rather than as a normative FOLDER archetype defined by the openEHR specifications.

The document is retained as a historical technical design note. It neither provides evidence of the executed Basic FOLDER proof of concept (T1) nor constitutes a complete or production-validated implementation.

## openEHR Reference Model basis

The example follows the openEHR Reference Model concept of a `FOLDER` as a named, archetypable structure that may contain:

-   nested `FOLDER` objects
-   `OBJECT_REF` references to other, usually versioned, EHR objects
-   optional archetypable metadata in `details`

The EHR's versioned FOLDER structure manages the hierarchy. Directory changes therefore have a lifecycle distinct from changes to the referenced clinical COMPOSITIONs.

The example uses `OBJECT_REF.type = VERSIONED_COMPOSITION` for the referenced objects.

## Archetype identifier in the example

The root uses the generic identifier:

`openEHR-EHR-FOLDER.generic.v1`

The identifier is retained from the generic FOLDER design in the thesis to indicate the archetyped nature of the example.

The example is a **representative manuscript artifact**. It does not imply that a separately governed or published CKM FOLDER archetype with this identifier belongs to the study’s clinical model set.

The child `archetype_node_id` values (`at0001` to `at0006`) are illustrative node identifiers for this representative hierarchy.

## Evidence boundary

This artifact illustrates the following design-level properties:

-   FOLDER can provide patient-level hierarchical navigation and indexing
-   existing EHR objects can be referenced rather than copied
-   the same clinical object can participate in multiple FOLDER organizations
-   Care Encounter-, Episode-, and Clinical Section-oriented navigation can coexist as alternative organizations over the same clinical record

This artifact does **not** demonstrate:

-   `DV_EHR_URI` references to individual ENTRYs or SECTIONs
-   runtime or query performance
-   production-scale directory management
-   concurrency behavior
-   usability of a FOLDER-based navigation interface
-   cross-repository reference resolution
-   multi-vendor interoperability
-   implementation of the complete synthetic record comprising 121 Medical Record Entries as a persisted FOLDER hierarchy

These limitations are consistent with the design-level evidence boundary defined in the manuscript.

## Traceability

This artifact provides representative FOLDER design evidence relevant to functional requirements US1–US8 in:

`../../04-functional-evaluation/functional-traceability.csv`

It also informs the architectural comparison of the FOLDER pattern, particularly patient-wide navigation, directory-based organization, independent versioning of the navigation structure, and reference-based access to existing EHR content.
