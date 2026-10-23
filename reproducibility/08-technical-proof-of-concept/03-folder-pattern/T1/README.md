# Basic FOLDER Pattern — Evaluated Scenario T1

**EHRbase:** 2.30.1. **EHR ID:** `8dcd91be-ccb2-4ace-8a18-88d9bd5bce5b`. **Root DIRECTORY ID:** `7961df16-9674-4959-8048-ea016c48dfcb`.

This is the FOLDER pattern used for the scientific evaluation. The initial DIRECTORY contains `Contacts` (CE1, CE2) and `Episodes` (EP1–EP4) branches. No separate Clinical Sections FOLDER hierarchy was implemented. Fifteen COMPOSITIONs were persisted separately (two Care Encounters, four Episodes of Care, and nine Medical Records). The initial relationship inventory comprised 33 references: nine Contact-to-Medical-Record COMPOSITION `OBJECT_REF` items, six FOLDER-to-context-COMPOSITION `DV_EHR_URI` references, and 18 Episode-to-clinical-content `DV_EHR_URI` references. Each SOAP note is referenced as one `SECTION.soap.v0` target rather than as four separate progress-note ENTRY targets.

## Request Artifacts (Renamed, JSON Bytes Unchanged)

| Official test | File | Intended operation | Evidence caveat |
|---|---|---|---|
| T1.3 | `tests/T1.3-directory-initial-POST.json` | Initial DIRECTORY POST | Initial persisted directory version `::1`, 33 references. |
| T1.6 | `tests/T1.6-directory-add-relationship-from-v1-PUT.json` | PUT payload carrying root UID version `::1` | Payload already contains the added EP3 → MR1 Pulse relationship. Do not interpret it as an unchanged v1→v2 request. Its first submission returned an error. The response history is needed to attribute subsequent DIRECTORY updates precisely. |
| T1.6 | `tests/T1.6-directory-add-relationship-from-v2-PUT.json` | PUT payload carrying root UID version `::2` | Adds EP3 → MR1 Pulse. Independently retrieved DIRECTORY `::3` contains 34 references. |
| T1.7 | `tests/T1.7-directory-remove-relationship-from-v3-PUT.json` | PUT payload carrying root UID version `::3` | Removes only EP3 → MR1 Pulse. An independent GET confirmed DIRECTORY `::4` with 33 references. |

**Important:** `from-vN` identifies the UID version in the submitted payload, not a guaranteed response version or proof of successful execution. The initial `::1` and final `::4` versions were independently retrieved. Intermediate response details are documented in [DOC-04](../../DOC-04-poc-results.md) and cannot be established from the JSON request files alone.

## Results and limitations

- Initial DIRECTORY POST and independent GET were successful.
- Multiple episode references to the same clinical target were persisted without duplicating clinical content.
- AQL retrieval of a selected Blood Pressure ENTRY and SOAP SECTION was successful. Native dereferencing of the stored `DV_EHR_URI` references was not demonstrated.
- Adding and removing a relationship through DIRECTORY updates succeeded while preserving the original clinical MR1 COMPOSITION. A duplicate `DbJsonPath` error was observed during an intermediate PUT. Its underlying cause was not established.
- Reconstruction of all eight clinician-centered views and reference resolution where multiple instances of the same archetype occur within one COMPOSITION were not systematically tested.
- `Primary` and `Associated` roles are not encoded by this Basic FOLDER representation.

For the complete test execution status and supporting evidence, see [DOC-04](../../DOC-04-poc-results.md). The JSON files in `tests/` are retained as request payloads. Their filenames identify documented test steps and intended operations.

AQL retrieval observations are documented in [DOC-04](../../DOC-04-poc-results.md). Complete AQL response payloads were not separately archived.
