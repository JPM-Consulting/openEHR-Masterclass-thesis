# Synthetic Patient Dataset

This directory contains the synthetic longitudinal patient record used as the common clinical dataset in the comparative design evaluation.

## Contents

``` text
03-synthetic-dataset/
├── README.md
├── synthetic-patient-medical-record.xlsx
└── synthetic-patient-medical-record.csv
```

The Excel workbook is the primary human-readable source. The CSV file provides a text-based representation of the same synthetic record for inspection and reuse.

## Purpose

The dataset provides a consistent clinical basis for assessing whether the three implementation patterns can support the clinician-centered views and retrieval requirements defined in the study. It is a purposively constructed, single-patient synthetic case, not a random or representative sample of patients, clinical settings, or workloads.

The same underlying patient history is used across the FOLDER-, LINK-, and CLUSTER-based designs. This keeps the clinical scenario constant while allowing the relationship representations to be compared.

The dataset is **synthetic** and contains no real patient data.

The synthetic longitudinal patient record comprises **121 Medical Record Entries**. Blank rows visually separate Care Encounters in the tabular files and are not counted as Medical Record Entries.

## Dataset structure

The record is organized chronologically and includes the following fields:

-   **Date**
-   **Contact**
-   **Detail entry**
-   **Section**
-   **Health problem / Episode of Care**
-   **ID**
-   **Condition**
-   **Clinical Status**
-   **Recording Timestamp**
-   **Event Timestamp**
-   **Availability Timestamp**

These fields support complementary views of the record by chronology, Care Encounter, Health Problem / Episode of Care, and Clinical Section.

The dataset includes diagnoses and problems, vital signs, laboratory results, medication-related information, progress notes, and other longitudinal clinical documentation.

## Role in the functional evaluation

The dataset provides the common patient history used to assess the eight clinician-centered functional requirements documented in:

`../04-functional-evaluation/functional-requirements.md`

The corresponding traceability matrix is available in:

`../04-functional-evaluation/functional-traceability.csv`

The functional evaluation assesses whether each implementation pattern can represent the relationships needed to derive the specified clinical views without duplicating the underlying clinical statements.

The dataset supports the **design-level evaluation**. Its controlled, shared case enables within-case comparison of relationship representations, but does not establish that the evaluated requirements cover the range of real-world clinical practice. It does not provide evidence of runtime performance.

## Relationship to the technical proof of concept

The 121-entry longitudinal dataset is the common clinical basis for the comparative design evaluation. The technical proof of concept uses a smaller, scenario-specific set of clinical records and context COMPOSITIONs. Its observed results must not be interpreted as execution or validation of all 121 Medical Record Entries. See the [technical PoC overview](../08-technical-proof-of-concept/README.md) and [PoC results](../08-technical-proof-of-concept/DOC-04-poc-results.md).

## Relationship to the conceptual model

The dataset illustrates the dimensions described in:

`../01-conceptual-model/`

In particular, individual clinical entries can be considered in relation to:

-   their chronological Care Encounter
-   their longitudinal Episode of Care / Health Problem
-   their Clinical Section

These dimensions remain conceptually distinct, even when the same clinical entry contributes to multiple views.

## Relationship to the implementation patterns

The underlying clinical content remains constant across the three evaluated patterns.

The implementation-pattern artifacts are located under:

``` text
../02-implementation-patterns/
├── folder/
├── link/
└── cluster/
```

The patterns differ in their representation of relationships and organizational structures. The comparison does not require three independent copies of the synthetic clinical record.

## Entry count

The synthetic dataset contains **121 Medical Record Entries**. This count excludes the blank rows separating Care Encounters in the tabular files.

When inspecting or processing either file, the total number of spreadsheet rows or CSV records should not be interpreted as the number of Medical Record Entries.

## File formats

### Excel

`synthetic-patient-medical-record.xlsx`

The Excel workbook preserves the tabular representation used in the design study and is intended primarily for human inspection.

### CSV

`synthetic-patient-medical-record.csv`

The CSV file supports text-based inspection and reuse. It uses semicolon delimiters and includes multiline text in some clinical entries.

Use a CSV parser that supports semicolon delimiters and quoted multiline fields. Individual physical lines must not be treated as separate records.

## Evidence boundary

The dataset serves as a synthetic design dataset for the comparative study.

Its inclusion does not establish:

-   validation against real patient records
-   completeness for all clinical specialties or care settings
-   clinical representativeness of a population
-   production-scale data volume
-   runtime or query-performance characteristics
-   usability or clinical outcome effects
-   empirical multi-vendor interoperability

The case provides internal consistency for the specified scenarios, not external clinical validity. Findings about representational feasibility in this case should not be generalized to other patients, care settings, clinical workflows, data distributions, or openEHR implementations without additional evaluation.

## Provenance and privacy

The patient history was created synthetically for this episode-oriented medical record study. Reproducing the documented design-level evaluation does not require real patient data.

## Manuscript mapping

The Methods and Results sections of the manuscript refer to this dataset as the common longitudinal patient history used in the functional evaluation.

Detailed manuscript-to-artifact traceability is maintained in:

`../07-manuscript-mapping/manuscript-artifact-mapping.md`
