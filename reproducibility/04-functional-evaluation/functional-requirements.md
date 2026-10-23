# Functional Requirements and Design-Level Support Criteria

## Purpose

This document defines the eight clinician-centered functional requirements used in the comparative evaluation reported in:

**Jean-Pierre Messerli. *Representing Episode-of-Care Relationships in openEHR: A Comparative Evaluation of Three Implementation Patterns.***

The requirements were formulated independently of a particular openEHR relationship mechanism and were evaluated against the same synthetic longitudinal patient medical record for all three implementation patterns:

1.  FOLDER-based organization
2.  LINK-based relationships
3.  CLUSTER-based relationship structures

This document defines the operational meaning of **Supported at design level**, as used in the manuscript and `functional-traceability.csv`. It specifies the minimum representational capabilities required for each functional requirement.

## Evaluation scope

The functional evaluation examines representational capability, not implementation performance or clinical usability.

A functional requirement is classified as **Supported at design level** when the represented clinical and relationship information is sufficient to construct the corresponding clinical view or organization without introducing another authoritative source of clinical content.

The following do **not**, on their own, indicate that a functional requirement is unsupported:

-   the need for reference resolution
-   a multi-step retrieval workflow
-   application-side assembly or projection of a view
-   differences in query structure between implementation patterns

These characteristics are assessed separately in the architectural evaluation.

Conversely, Supported at design level does not mean that:

-   a complete production implementation was deployed
-   an end-user interface was implemented or evaluated
-   runtime performance was benchmarked
-   clinical usability was evaluated
-   multi-vendor or cross-repository interoperability was empirically demonstrated
-   every required view can necessarily be produced by one AQL statement

The evaluation therefore assesses whether each pattern can represent the relationships and classifications needed to derive the eight functional views while preserving the common clinical information model.

The eight positive classifications establish representational feasibility under the shared design assumptions. They do not demonstrate that the patterns offer equivalent relationship semantics, retrieval effort, implemented functionality, or clinical workflows. These distinctions are examined through the architectural evaluation and the documented proof-of-concept evidence boundaries.

## Common evaluation basis

All eight requirements are evaluated against the same synthetic longitudinal dataset:

`../03-synthetic-dataset/synthetic-patient-medical-record.xlsx`

The dataset contains 121 synthetic Medical Record Entries distributed across multiple Care Encounters and Episodes of Care and includes acute and chronic clinical trajectories.

All three implementation patterns use the same underlying clinical information. The patterns differ in how relationships are represented, governed, navigated, and retrieved. They do not use separate clinical datasets.

The common information model distinguishes:

-   **Care Encounter (Contact)** as the chronological care-event dimension
-   **Episode of Care** as the longitudinal representation of one distinct Health Problem
-   **Administrative Encounter** as the organizational care-period dimension
-   **Clinical Section** as an additional semantic classification dimension
-   **Medical Record Entry** as the individual clinical statement or recorded clinical information

Clinical statements remain represented in their source clinical ENTRYs and COMPOSITIONs. The evaluated relationship mechanisms provide alternative ways of associating and organizing that information.

---

## US1 --- Chronological retrieval by Care Encounter

### Functional requirement

A healthcare professional must be able to obtain the patient's clinical information in chronological order and grouped by Care Encounter.

### Clinical intent

This view answers the question:

> **What clinical information was documented during each successive Care Encounter?**

Chronological organization is distinct from longitudinal Episode-of-Care organization. A Care Encounter may contain information relating to more than one Health Problem.

### Design-level support criterion

The requirement is **Supported at design level** when:

1.  clinical information can be associated with the Care Encounter in which it was documented
2.  Care Encounters can be ordered chronologically
3.  the Medical Record Entries associated with each Care Encounter can be identified or retrieved
4.  the resulting chronological view can be constructed without duplicating the underlying clinical statements into a separate authoritative record

The association may be represented directly or obtained through traversal or reference resolution.

### Evidence boundary

Support demonstrates that the chronological Care Encounter view is derivable from the represented information. It does not demonstrate an implemented chronological user interface, retrieval performance, or clinical usability.

---

## US2 --- Episode-oriented retrieval for a selected Health Problem

### Functional requirement

A healthcare professional must be able to select an Episode of Care and obtain the clinical information associated with the corresponding Health Problem across multiple Care Encounters.

### Clinical intent

This view answers the question:

> **What clinical information belongs longitudinally to this Health
> Problem, irrespective of the Care Encounter in which it was
> documented?**

The Episode-oriented view organizes existing clinical information by longitudinal Health Problem context without creating an Episode-specific copy.

### Design-level support criterion

The requirement is **Supported at design level** when:

1.  an Episode of Care can be represented as the longitudinal representation of a distinct Health Problem
2.  clinical information can be associated with the relevant Episode of Care
3.  associations can extend across multiple Care Encounters
4.  the Medical Record Entries associated with a selected Episode can be identified or retrieved
5.  the Episode-oriented view can be constructed without duplicating the source clinical statements into a separate authoritative Episode record

Where clinically required, the design may distinguish a primary Episode association from additional associated Episodes.

For the evaluated FOLDER T1 design, Episode membership satisfies this requirement without encoding Primary and Associated relationship roles. The evaluated LINK and CLUSTER designs can represent these roles explicitly. Accordingly, the shared positive US2 classification applies to Episode membership and retrieval, not to equivalent role semantics across the three patterns.

### Evidence boundary

Support demonstrates representational capability for longitudinal Episode reconstruction. It does not demonstrate cross-repository Episode retrieval, query performance, or a production Episode-oriented user interface.

---

## US3 --- Organization by Clinical Section

### Functional requirement

A healthcare professional must be able to organize the patient's clinical information according to standard Clinical Sections.

### Clinical intent

Clinical Section provides a semantic classification dimension that is independent of both Care Encounter and Episode of Care. Examples include medical history, physical examination, diagnostics, therapy, risk factors, and progress information.

This view answers the question:

> **What information of a particular clinical type or section is present in the longitudinal record?**

### Design-level support criterion

The requirement is **Supported at design level** when:

1.  Medical Record Entries can be assigned to an appropriate Clinical Section
2.  Clinical Section classification is retained independently of Care Encounter and Episode-of-Care organization
3.  clinical information belonging to a selected Clinical Section can be identified or retrieved
4.  the section-oriented view can be constructed from existing clinical information without creating a second authoritative copy

### Evidence boundary

Support demonstrates that Clinical Section classification and section-oriented retrieval are representable. It does not demonstrate an implemented section-based user interface, terminology completeness for all possible clinical sections, or usability.

---

## US4 --- Combined Clinical Section × Care Encounter/Episode views

### Functional requirement

A healthcare professional must be able to combine Clinical Section organization with either Care Encounter context or Episode-of-Care context.

### Clinical intent

The same clinical information must be viewable across more than one contextual dimension.

Examples include:

-   diagnostic information associated with a selected Health Problem across several Care Encounters
-   clinical information generated during one Care Encounter organized by Clinical Section

This requirement assesses whether the model preserves the distinctness of the chronological, longitudinal Health Problem, and Clinical Section dimensions while allowing them to be combined.

### Design-level support criterion

The requirement is **Supported at design level** when:

1.  Clinical Section classification can coexist with Care Encounter and Episode-of-Care associations
2.  the same Medical Record Entry can retain the contextual information required for these dimensions
3.  information can be selected using a combination of Clinical Section and Care Encounter or Episode context
4.  combined views can be constructed without creating context-specific copies of the underlying clinical statements

### Evidence boundary

Support demonstrates that multidimensional projections are representable and derivable. It does not demonstrate a particular user-interface interaction model, comparative query efficiency, or performance of combined filtering.

---

## US5 --- Linear Diagnosis and Problem Lists

### Functional requirement

A healthcare professional must be able to obtain two distinct linear longitudinal views of the patient's Episodes of Care: a Diagnosis List comprising Episode-of-Care COMPOSITIONs with `Classification = Diagnosis`, and a Problem List comprising Episode-of-Care COMPOSITIONs with `Classification = Problem`.

### Clinical intent

Both lists are derived views over existing Episode-of-Care COMPOSITIONs, rather than separately maintained authoritative copies. Each Episode of Care represents one distinct Health Problem. The `Classification` attribute determines inclusion in the respective view.

These views answer the questions:

- Which Episodes of Care are classified as diagnoses?
- Which Episodes of Care are classified as problems?

### Design-level support criterion

The requirement is **Supported at design level** when:

1. Episode-of-Care COMPOSITIONs are individually identifiable and associated with the patient
2. each Episode-of-Care COMPOSITION retains an accessible `Classification` attribute distinguishing `Diagnosis` and `Problem`
3. the set of Episode-of-Care COMPOSITIONs can be identified or retrieved and filtered by that classification
4. two separate linear views can be derived from the corresponding Episode-of-Care COMPOSITIONs
5. neither view requires a second authoritative copy of the Episode-of-Care clinical content

### Evidence boundary

Support demonstrates that the two classification-based linear views are representable and derivable at design level. It does not establish that both complete lists were generated and validated in the technical proof of concept, nor does it validate their presentation, ordering, or clinical usability.

---

## US6 --- Hierarchical Diagnosis and Problem List

### Functional requirement

A healthcare professional must be able to create and maintain a clinician-curated hierarchical Diagnosis and Problem List, represented in a **separate COMPOSITION** containing references to existing Episode-of-Care COMPOSITIONs and explicitly documenting their hierarchical organization.

### Clinical intent

This requirement is distinct from US5. The two US5 lists are linear views derived by filtering Episode-of-Care COMPOSITIONs on `Classification`. US6 concerns a separately documented, clinician-curated hierarchy of those Episodes of Care.

The hierarchical-list COMPOSITION stores the organizational structure and references to the relevant Episode-of-Care COMPOSITIONs without duplicating their authoritative clinical content. Its hierarchy cannot be inferred solely from the `Classification` attribute.

### Design-level support criterion

The requirement is **Supported at design level** when:

1. a separate COMPOSITION can represent a persistent, clinician-curated hierarchical organization
2. that COMPOSITION can reference identifiable Episode-of-Care COMPOSITIONs
3. the hierarchy's grouping, ordering, or parent–child relationships can be represented explicitly
4. the hierarchy can be revised without duplicating or replacing the authoritative clinical content in the referenced Episode-of-Care COMPOSITIONs
5. the curated hierarchical list remains distinguishable from the two derived linear lists defined in US5

### Evidence boundary

Support demonstrates design-level representability of a separate hierarchical-list COMPOSITION and its references to Episode-of-Care COMPOSITIONs. It does **not** establish that this separate COMPOSITION, its complete hierarchy, or its editing workflow was implemented or technically validated for all three patterns. Nor does it demonstrate collaborative curation, conflict resolution, user-interface usability, or clinical validation of a particular hierarchy.

---

## US7 --- SOAP-oriented documentation for one or more Health Problems

### Functional requirement

A healthcare professional must be able to organize progress documentation according to the SOAP structure and associate that documentation with one or more Health Problems.

### Clinical intent

SOAP-oriented documentation distinguishes:

-   **Subjective**
-   **Objective**
-   **Assessment**
-   **Plan**

A progress note may concern one primary Health Problem and may also relate to additional associated Health Problems.

The requirement assesses whether SOAP classification and longitudinal Health Problem context can coexist without requiring copies of the underlying clinical information.

### Design-level support criterion

The requirement is **Supported at design level** when:

1.  relevant clinical information can be assigned to the appropriate SOAP category
2.  SOAP-oriented information can be associated with at least one Episode of Care
3.  additional Episode associations can be represented where the same documentation is clinically relevant to more than one Health Problem
4.  primary and associated Episode roles can be distinguished where required by the evaluated design
5.  SOAP-oriented views can be constructed while the underlying clinical statements remain in their source ENTRYs and COMPOSITIONs

### Evidence boundary

Support demonstrates that SOAP classification and Episode associations can be represented together. It does not demonstrate a complete clinical documentation workflow, user-interface behavior, clinical decision support, or usability of SOAP documentation.

---

## US8 --- Section-oriented patient dashboards

### Functional requirement

A healthcare professional must be able to obtain patient-level dashboard views in which individual widgets or projections display clinical information belonging to selected Clinical Sections.

### Clinical intent

This requirement assesses whether the represented information can support application-level projections of the longitudinal record.

A dashboard widget may, for example, present information from a particular Clinical Section while preserving the underlying Care Encounter and Episode-of-Care context for further navigation or filtering.

### Design-level support criterion

The requirement is **Supported at design level** when:

1.  the clinical information required for a dashboard projection can be identified through its Clinical Section classification
2.  the relevant Medical Record Entries can be retrieved or selected from the longitudinal record
3.  the dashboard view can be constructed as a query or application projection over existing clinical information
4.  no separate authoritative dashboard-specific copy of the clinical statements is required

### Evidence boundary

Support demonstrates availability of the information required to construct section-oriented dashboard projections. It does not demonstrate an implemented dashboard, visualization quality, interaction design, usability, response time, or clinical effectiveness.

---

## Interpretation of the functional evaluation

The functional evaluation applies the same support criterion to FOLDER, LINK, and CLUSTER.

A pattern is not required to use the same retrieval mechanism as another pattern. In particular, reference resolution, directory traversal, or application-side projection may be required depending on where relationship information is represented.

Functional adequacy and architectural characteristics are therefore evaluated separately.

The classification:

> **Supported at design level**

means that the information required for the functional requirement can be represented and obtained using the evaluated pattern together with the common information model and synthetic dataset, without introducing an additional authoritative source of clinical content.

It does **not** establish architectural or functional equivalence among the patterns, nor does it establish that all eight clinical workflows were implemented and tested end to end.

Differences in semantic governance, navigation, query workflow, versioning and provenance, implementation responsibility, and cross-system dependencies are addressed separately in the architectural evaluation.

## Relationship to manuscript Table 1

The eight requirements defined above correspond to the functional requirements reported in Table 1 of the manuscript:

| ID | Functional requirement | Manuscript result |
| --- | --- | --- |
| US1 | Chronological retrieval by Care Encounter | Supported by FOLDER, LINK, and CLUSTER at design level |
| US2 | Episode-oriented retrieval for a selected Health Problem | Supported by FOLDER, LINK, and CLUSTER at design level |
| US3 | Organization by Clinical Section | Supported by FOLDER, LINK, and CLUSTER at design level |
| US4 | Combined Clinical Section × Care Encounter/Episode views | Supported by FOLDER, LINK, and CLUSTER at design level |
| US5 | Linear Diagnosis and Problem Lists | Supported by FOLDER, LINK, and CLUSTER at design level |
| US6 | Hierarchical Diagnosis and Problem List | Supported by FOLDER, LINK, and CLUSTER at design level |
| US7 | SOAP-oriented documentation for one or more Health Problems | Supported by FOLDER, LINK, and CLUSTER at design level |
| US8 | Section-oriented patient dashboards | Supported by FOLDER, LINK, and CLUSTER at design level |

The detailed evidence connecting each requirement to the synthetic dataset, common information model, implementation patterns, modeling artifacts, and evidence boundaries is provided in:

`functional-traceability.csv`

The traceability matrix is provided in two equivalent formats. `functional-traceability.csv` is the authoritative, machine-readable source. `functional-traceability.xlsx` contains the same evaluation data, with reader-friendly column headings and spreadsheet navigation features for convenient inspection and review. The Excel file is a presentation of the CSV data, not an independent evaluation or additional evidence.

## Versioning and authority

This document specifies how the eight functional requirements are operationalized for the manuscript.

Where wording or interpretation differs from earlier versions in the underlying Masterclass thesis, this document and the final manuscript represent the authoritative formulation for the published comparative evaluation.
