# LINK Retrieval Workflow

## Purpose

This document describes representative retrieval workflows for the LINK-based implementation pattern examined in the study.

It should be read together with:

-   `../../02-implementation-patterns/link/care-encounter-links.json`
-   `../../02-implementation-patterns/link/episode-of-care-links.json`
-   `../../02-implementation-patterns/link/README.md`
-   `../README.md`

The examples illustrate **logical relationship traversal and target resolution**. They do not establish a portable single-statement AQL solution or provide measured query-performance evidence.

## Retrieval principle

An openEHR LINK is an attribute of its owning LOCATABLE and represents a relationship with a target reference.

The representative retrieval workflow is:

``` text
1. Retrieve or identify the source object
        ↓
2. Inspect the relevant LINK
        ↓
3. Interpret relationship meaning and type
        ↓
4. Obtain the DV_EHR_URI target
        ↓
5. Resolve the target when target content is required
        ↓
6. Retrieve or project the required target information
```

Identifying a relationship and retrieving information stored only in its target are distinct operations.

## Example 1: Care Encounter to clinical COMPOSITION

### Clinical question

Identify the clinical COMPOSITIONs associated with a selected Care Encounter.

### Representative relationship

The artifact:

`../../02-implementation-patterns/link/care-encounter-links.json`

illustrates alternative relationship directions between a Care Encounter COMPOSITION and a clinical COMPOSITION.

One direction is illustrated below:

``` text
Care Encounter COMPOSITION
        ↓
      LINK
        ├── meaning
        ├── type
        └── target: DV_EHR_URI
                         ↓
              clinical COMPOSITION
```

### Logical workflow

1.  identify the Care Encounter COMPOSITION
2.  inspect the relevant LINK relationship
3.  obtain the target URI
4.  resolve the referenced clinical COMPOSITION
5.  retrieve the required clinical content from that COMPOSITION

The artifact also illustrates the reverse relationship direction as an alternative configuration.

The examples do not imply that both directions must be persisted. Relationship direction is an implementation and governance decision.

## Example 2: Clinical ENTRY to primary Episode of Care

### Clinical question

Identify the primary Episode of Care for a clinical ENTRY.

### Representative relationship

The artifact:

`../../02-implementation-patterns/link/episode-of-care-links.json`

illustrates an ENTRY-to-Episode relationship.

``` text
clinical ENTRY
      ↓
    LINK
      ├── meaning
      ├── type = episode-of-care-primary
      └── target: DV_EHR_URI
                       ↓
            Episode-of-Care COMPOSITION
```

### Logical workflow

1.  identify the relevant clinical ENTRY
2.  inspect its Episode relationship LINK
3.  interpret the relationship convention as the primary Episode association
4.  obtain the Episode target URI
5.  resolve the Episode-of-Care COMPOSITION when Episode target information is required

The `type` value in the artifact is a convention of the evaluated design, not a universally standardized openEHR relationship type.

## Example 3: Clinical ENTRY with an additional associated Episode

### Clinical question

Identify an additional Episode of Care associated with the same clinical ENTRY.

The design allows multiple Episode associations where clinically appropriate.

``` text
clinical ENTRY
      ├── LINK → primary Episode of Care
      └── LINK → associated Episode of Care
```

The representative artifact distinguishes primary and associated roles using design-specific relationship conventions.

The clinical statement remains in its source ENTRY while being associated with multiple longitudinal Health Problem contexts.

## Example 4: Episode of Care to clinical ENTRY

The repository artifact also illustrates a reverse-direction alternative:

``` text
Episode-of-Care COMPOSITION
        ↓
      LINK
        └── target: DV_EHR_URI
                         ↓
                   clinical ENTRY
```

This example highlights relationship direction and granularity as explicit design decisions.

The design does not require forward and reverse variants to be persisted simultaneously.

## Target resolution

A LINK target identifies another EHR object or path.

When the required information exists only in the referenced target, the application must resolve that target to retrieve it.

For example:

``` text
LINK.target
   ↓
DV_EHR_URI
   ↓
resolve target
   ↓
read target attributes
```

This distinction underlies the manuscript's separation of **relationship traversal** from **target resolution**.

## Why no portable single-statement AQL file is provided here

The reproducibility package does not establish that traversing LINK relationships and dereferencing arbitrary `DV_EHR_URI` targets can be performed in a single portable AQL statement across openEHR CDR implementations.

A syntactically plausible query would not, by itself, establish such portability.

The LINK examples therefore document:

-   the source relationship
-   the relationship attributes
-   the target URI
-   the required resolution step

without presenting pseudocode as evidence of an executed query.

## Versioning implication

A LINK belongs to its owning LOCATABLE.

In the evaluated design, when a LINK is stored within a version-controlled COMPOSITION, changes to that relationship follow the version lifecycle of the owning COMPOSITION.

By contrast, changes to the FOLDER-based Directory organization are versioned separately from the referenced clinical COMPOSITIONs.

## Cross-system implication

Target resolvability alone does not ensure consistent cross-system interpretation.

Cross-system use also requires agreement on relationship semantics and conventions, including:

-   relationship meaning
-   relationship type
-   direction
-   target selection
-   relationship granularity
-   target-resolution mechanism

The study does not empirically validate cross-CDR or multi-vendor LINK resolution.

## Evidence boundary

The examples illustrate the following retrieval sequence for the LINK pattern:

**source object → relationship traversal → DV_EHR_URI target → target resolution where required**

The representative artifacts illustrate the design-level representation of:

-   Care Encounter-to-clinical-COMPOSITION relationships
-   clinical-ENTRY-to-Episode relationships
-   primary and associated Episode roles through the evaluated design conventions
-   alternative relationship directions

They do not demonstrate:

-   universal AQL dereferencing
-   query-performance characteristics
-   automatic target resolution
-   cross-CDR resolution
-   multi-vendor semantic interoperability
-   a requirement to persist both relationship directions
-   universal standardization of the manuscript-specific `type` values

These examples document representative retrieval workflows at the design level. They are not evidence of executed end-to-end retrieval or comparative runtime behavior.
