# FOLDER Retrieval Workflow

## Purpose

This document describes representative retrieval workflows for the FOLDER-based implementation pattern examined in the study.

It should be read together with:

-   `../../02-implementation-patterns/folder/folder-example.json`
-   `../../02-implementation-patterns/folder/README.md`
-   `../README.md`

These examples describe **logical retrieval workflows**. They are not portable single-statement AQL queries and do not provide evidence of measured retrieval performance.

## Retrieval principle

In the evaluated FOLDER pattern, the EHR Directory organizes references to existing EHR objects at the patient level.

Retrieval therefore involves two conceptually distinct operations: Directory navigation and resolution of referenced EHR objects. The workflow can be summarized as follows:

``` text
1. Navigate the Directory
        ↓
2. Select the relevant FOLDER
        ↓
3. Obtain the references indexed by that FOLDER
        ↓
4. Resolve the referenced EHR objects
        ↓
5. Retrieve or project the required clinical information
```

The FOLDER hierarchy serves as an organizational index without duplicating the referenced clinical content.

## Example 1: Episode-oriented retrieval

### Clinical question

Retrieve clinical information indexed under a selected Episode of Care (Health Problem).

### Logical workflow

``` text
EHR
└── Directory
    └── Episodes of Care
        └── selected Episode
            ├── reference → clinical object A
            ├── reference → clinical object B
            └── reference → clinical object C
```

The application identifies the Episode-oriented branch and the FOLDER representing the selected Episode of Care.

The application then resolves the FOLDER references to their target EHR objects and retrieves the required clinical information.

### Interpretation

The Episode FOLDER provides a navigation and indexing structure for information associated with the Episode of Care. The referenced clinical ENTRYs and COMPOSITIONs remain the authoritative source of clinical statements.

The same clinical object can be indexed in other organizational views without duplicating its clinical content.

## Example 2: Care Encounter-oriented retrieval

### Clinical question

Retrieve clinical information indexed under a selected Care Encounter.

### Logical workflow

``` text
EHR
└── Directory
    └── Care Encounters
        └── selected Care Encounter
            ├── reference → clinical object A
            └── reference → clinical object B
```

The application navigates to the Care Encounter branch, selects the relevant FOLDER, and resolves its references to the target EHR objects.

A chronological view can be derived by ordering the relevant Care Encounters using their modeled temporal information.

## Example 3: Clinical Section-oriented retrieval

### Clinical question

Retrieve clinical information indexed under a selected Clinical Section.

### Logical workflow

``` text
EHR
└── Directory
    └── Clinical Sections
        └── selected Clinical Section
            ├── reference → clinical object A
            ├── reference → clinical object D
            └── reference → clinical object E
```

The same clinical object may also be indexed under Care Encounter- or Episode-oriented branches.

This illustrates how FOLDER can organize multiple patient-level views over existing clinical content without duplicating it.

## Representative artifact

The repository artifact `../../02-implementation-patterns/folder/folder-example.json` illustrates Care Encounter-, Episode-, and Clinical Section-oriented branches with references to existing EHR objects.

The example is intentionally limited in scope. It does not represent a persisted Directory containing the complete synthetic longitudinal patient record.

## Why no AQL file is provided here

The architectural evaluation of FOLDER focuses on **Directory traversal and reference resolution**.

Accordingly, this reproducibility package does not substitute an illustrative AQL statement for the complete FOLDER retrieval workflow.

The absence of a FOLDER AQL example does not imply that AQL cannot be used in an implementation involving FOLDER. The study does not claim or demonstrate a portable single-statement AQL workflow for the Directory navigation and reference-resolution process.

## Versioning implication

The FOLDER hierarchy is part of the EHR Directory, which is managed as a `VERSIONED_FOLDER`.

The complete Directory hierarchy, rather than an individual FOLDER subtree, is the unit of versioning.

Changes to this organizational hierarchy can be versioned independently of the referenced clinical content.

For retrieval, the Directory thus provides a versioned organizational view over clinical objects with their own version histories.

## Evidence boundary

The example illustrates the following retrieval sequence in the evaluated FOLDER design:

**Directory traversal → FOLDER selection → reference resolution → target retrieval**

It does not demonstrate:

-   retrieval latency or throughput
-   production-scale Directory behavior
-   an implemented navigation user interface
-   universal query portability
-   automatic synchronization of FOLDER membership
-   cross-repository reference resolution
-   superiority or inferiority relative to LINK or CLUSTER

The example documents the proposed retrieval workflow at the design level. It is not evidence of an executed end-to-end retrieval test or a performance experiment.
