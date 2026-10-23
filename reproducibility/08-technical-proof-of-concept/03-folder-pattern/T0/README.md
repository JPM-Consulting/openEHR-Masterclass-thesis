# Preliminary FOLDER Feasibility Test (T0)

## Purpose and scope

T0 is an isolated preliminary feasibility test of relationships represented using the openEHR `FOLDER` structure. It precedes the systematic T1 Basic FOLDER evaluation and is neither an additional implementation pattern nor evidence of T1 completion.

The test examines whether EHRbase can persist and retrieve a DIRECTORY hierarchy, COMPOSITION references, and ENTRY-level episode-of-care references. Unlike the subsequently evaluated Basic FOLDER pattern, T0 also uses exploratory relationship `CLUSTER` structures to associate ENTRY references with locally coded `Primary` and `Associated` roles. These role annotations are not part of the Basic FOLDER pattern assessed in T1.

## Environment and test data

- **CDR:** EHRbase 2.30.1
- **Interface and representation:** openEHR REST API and canonical JSON
- **Isolated test EHR:** `d95b9e3d-758b-4e8d-9b88-757290c2653f`
- **DIRECTORY root:** `9b073e8e-31c5-4558-833f-3ca23c5aa5df`
- **Scope:** Contact FOLDER CE1, Episode-of-Care FOLDERs EP1–EP4, and references to six existing COMPOSITIONs (CE1, EP1–EP4, MR1). Three ENTRY-level episode relationships were tested.

This test EHR is separate from the baseline validation EHR and the later T1 EHR.

## Test sequence and artifacts

| Step | JSON request payload | Observed outcome |
| --- | --- | --- |
| T0.1 | `tests/T0-folder-smoke-test.json` | Initial DIRECTORY hierarchy created and independently retrieved. PASS. DIRECTORY `::1`. |
| T0.2 | `tests/T0.2-folder-composition-references.json` | COMPOSITION references in `FOLDER.items` and `FOLDER.details` persisted and independently retrieved. PASS. DIRECTORY `::2`. |
| T0.3 – initial attempt | `tests/T0.3-folder-entry-relationships.json` | Request failed with HTTP 400 during URI deserialization because the ENTRY path contained unescaped `[` and `]`. FAIL (diagnostic attempt). |
| T0.3 – corrected | `tests/T0.3-folder-entry-relationships-URI-encoded.json` | Encoding the ENTRY path brackets as `%5B` and `%5D` resolved the syntax error. Relationship `CLUSTER`s were persisted and independently retrieved. PASS. DIRECTORY `::3`. |

The filenames identify request payloads, not saved HTTP responses. For observed outcomes and limitations, consult [`DOC-04-poc-results.md`](../../DOC-04-poc-results.md), section “Preliminary FOLDER Feasibility Test — T0”.

## Verified relationship examples

| Relationship | Meaning | Representation |
| --- | --- | --- |
| CR-001 | CE1 → MR1 clinical COMPOSITION | `FOLDER.items` / `OBJECT_REF` |
| CR-010 | MR1 Blood Pressure ENTRY → EP1 (`Primary`) | `FOLDER.details` / relationship `CLUSTER` containing `DV_EHR_URI` and role |
| CR-011 | Same MR1 Blood Pressure ENTRY → EP3 (`Associated`) | `FOLDER.details` / relationship `CLUSTER` containing `DV_EHR_URI` and role |
| CR-012 | MR1 Pulse ENTRY → EP1 (`Primary`) | `FOLDER.details` / relationship `CLUSTER` containing `DV_EHR_URI` and role |

The same Blood Pressure ENTRY was referenced in two episode contexts without duplicating its clinical content.

## Technical observations

- `FOLDER.folders` retained the Contact/Episode hierarchy.
- `FOLDER.items` stored a COMPOSITION-level `OBJECT_REF` (`VERSIONED_COMPOSITION`, namespace `local`).
- `FOLDER.details` stored COMPOSITION references as `DV_EHR_URI` values and, in this exploratory test, repeatable `CLUSTER` structures pairing an ENTRY `DV_EHR_URI` with a locally coded relationship role.
- A separate HTTP 400 observed during T0.2 was caused by an unset Postman variable (`VersionCompositionId`). The unchanged payload succeeded after the variable was configured.
- The final DIRECTORY version `9b073e8e-31c5-4558-833f-3ca23c5aa5df::local.ehrbase.org::3` was confirmed by an independent GET.

## Conclusions and limitations

**T0 overall: PASS** (T0.1–T0.3, following correction of the failed T0.3 request). The test demonstrated persistence and retrieval of the proposed FOLDER hierarchy, COMPOSITION references, and three ENTRY-level episode relationships in EHRbase 2.30.1 without modifying the openEHR Reference Model.

This does not establish native `DV_EHR_URI` dereferencing, automatic target-path resolution, referential integrity enforcement, or semantic validity of the targets. The local relationship codes and metadata node identifiers were not independently validated against governed archetype or terminology bindings. T0 did not reconstruct the complete clinician-centred views or evaluate the full clinical relationship dataset.

The systematically evaluated FOLDER implementation is documented under [`T1/`](../T1/). Further exploration of role-bearing relationship `CLUSTER`s is documented under [`exploratory-extension/`](../exploratory-extension/) and is not part of the evaluated Basic FOLDER pattern.

## Evidence files

This document is located at `03-folder-pattern/T0/README.md`. The four referenced request payloads are stored in `tests/`. The additional source file `T0-folder-template.json` is not included in this minimal evidence set because it is not tied to a uniquely documented successful test step.
