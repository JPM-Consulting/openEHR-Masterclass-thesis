# T1 – Basic FOLDER Pattern: Test EHR and Object Identifiers

**Purpose:** Identifier inventory for continuing or repeating tests against the isolated T1 EHR. The identifiers are drawn from the recorded Basic FOLDER PoC results. This document does not constitute a new live-server verification.

## Test environment

| Property | Value |
| --- | --- |
| Official PoC scenario | T1 – FOLDER-Based Relationships (Basic) |
| EHRbase version | `2.30.1` |
| System ID | `local.ehrbase.org` |
| EHR ID | `8dcd91be-ccb2-4ace-8a18-88d9bd5bce5b` |
| EHR_STATUS UID | `d9c2ffe4-30fb-484d-8831-878c0390c6e7::local.ehrbase.org::1` |
| REST API base URL (local test environment) | `http://localhost:8080/ehrbase/rest/openehr/v1` |
| COMPOSITIONs | 15 (2 Care Encounters, 4 Episodes of Care, 9 Medical Records) |
| Current documented root DIRECTORY version | `::4`, after relationship removal in T1.7 |
| Current documented relationship references | 33 (9 Contact → Medical Record, 6 FOLDER → context COMPOSITION, 18 Episode → clinical content) |

## COMPOSITION inventory

All 15 COMPOSITIONs were originally persisted as version `::1`. The `Versioned COMPOSITION UID` column provides the complete identifier for GET requests.

| ID | Type | Clinical description | COMPOSITION UUID | Versioned COMPOSITION UID |
| --- | --- | --- | --- | --- |
| CE1 | Care Encounter | Initial Consultation | `7d94b831-a3f9-4dcc-9357-76017c798de1` | `7d94b831-a3f9-4dcc-9357-76017c798de1::local.ehrbase.org::1` |
| CE2 | Care Encounter | Follow-up Consultation | `7fe11fce-0f8f-496f-b947-7c545a59bfb4` | `7fe11fce-0f8f-496f-b947-7c545a59bfb4::local.ehrbase.org::1` |
| EP1 | Episode of Care | General Health Problem (default episode) | `e6746cc1-372c-4a95-b078-51b66f50b1b1` | `e6746cc1-372c-4a95-b078-51b66f50b1b1::local.ehrbase.org::1` |
| EP2 | Episode of Care | Urinary Tract Infection | `5d96fcf0-5988-4649-a70b-0b05b4f89133` | `5d96fcf0-5988-4649-a70b-0b05b4f89133::local.ehrbase.org::1` |
| EP3 | Episode of Care | Arterial Hypertension | `99ebe958-d9a9-4fd0-ac49-ca0b2db241f0` | `99ebe958-d9a9-4fd0-ac49-ca0b2db241f0::local.ehrbase.org::1` |
| EP4 | Episode of Care | Obesity WHO Grade I | `e0df43fe-f506-47ad-90ec-3e5a480cb5f5` | `e0df43fe-f506-47ad-90ec-3e5a480cb5f5::local.ehrbase.org::1` |
| MR1 | Medical Record | Vital Signs – CE1 | `a5b1e471-f28f-4365-b0b0-51c1fb03b112` | `a5b1e471-f28f-4365-b0b0-51c1fb03b112::local.ehrbase.org::1` |
| MR2 | Medical Record | Body Measurements – CE1 | `93e1160d-c364-4cb5-b15b-5a12ab6a5024` | `93e1160d-c364-4cb5-b15b-5a12ab6a5024::local.ehrbase.org::1` |
| MR3 | Medical Record | Urinalysis – CE1 | `6a93d5f8-78b5-4df0-b699-5b3580d6112b` | `6a93d5f8-78b5-4df0-b699-5b3580d6112b::local.ehrbase.org::1` |
| MR4 | Medical Record | SOAP Progress Note – CE1 | `d524a132-ea78-41a8-b112-10a2ed795ea4` | `d524a132-ea78-41a8-b112-10a2ed795ea4::local.ehrbase.org::1` |
| MR5 | Medical Record | Medication Order – CE1 | `a731f2a6-cd0c-4386-a419-ff872889d9d1` | `a731f2a6-cd0c-4386-a419-ff872889d9d1::local.ehrbase.org::1` |
| MR6 | Medical Record | Microbiology Result – CE2 | `3ffb2e64-1a13-4adf-94c3-e050ceaa609b` | `3ffb2e64-1a13-4adf-94c3-e050ceaa609b::local.ehrbase.org::1` |
| MR7 | Medical Record | Vital Signs – CE2 | `983478c2-1060-4fc8-b534-7eb7ed6cee6a` | `983478c2-1060-4fc8-b534-7eb7ed6cee6a::local.ehrbase.org::1` |
| MR8 | Medical Record | SOAP Progress Note – CE2 | `efc0672a-51b9-4722-99b1-bb4d92b0a8cd` | `efc0672a-51b9-4722-99b1-bb4d92b0a8cd::local.ehrbase.org::1` |
| MR9 | Medical Record | Medication Order – CE2 | `4df8bcde-5b89-4df4-b47b-1eb7080dad9d` | `4df8bcde-5b89-4df4-b47b-1eb7080dad9d::local.ehrbase.org::1` |

## DIRECTORY identifiers and state

| Property | Value |
| --- | --- |
| Root DIRECTORY UUID | `7961df16-9674-4959-8048-ea016c48dfcb` |
| Latest documented root DIRECTORY UID | `7961df16-9674-4959-8048-ea016c48dfcb::local.ehrbase.org::4` |
| Version `::1` | Initial 33 references |
| Version `::2` | 33 references, with no change to the EP3 clinical relationship set |
| Version `::3` | 34 references, with an additional EP3 → MR1 Pulse relationship |
| Version `::4` | 33 references, after the additional EP3 → MR1 Pulse relationship removed, EP1 → MR1 Pulse retained |

### FOLDER UUIDs

| FOLDER | UUID |
| --- | --- |
| Contacts | `c71a3fa1-04b5-4ce9-ade1-2d2cdc3aca25` |
| CE1 | `27c818f0-53a1-4ed3-ad5e-68f35281e53d` |
| CE2 | `5376001a-3218-442d-b0ea-799b33638eb5` |
| Episodes | `f9245005-07e6-43ff-9968-d4102767924b` |
| EP1 | `bccf654c-e4d4-4210-9d57-279f1a635f86` |
| EP2 | `75babb4f-75c0-4b49-8d20-30cf7372baa9` |
| EP3 | `16d371c2-f299-4cf8-b64f-fa0e4bddd54e` |
| EP4 | `af6425fd-b940-4fd0-afb4-0529b6bdc0ad` |

## Reusing the test EHR

The recorded test state is DIRECTORY `::4`. Before performing additional changes, retrieve the current DIRECTORY and check its UID and version. Subsequent tests may have created a later version. Use the retrieved current state as the basis for subsequent updates rather than assuming `::4` remains current.

Example requests (Postman or equivalent):

```http
GET http://localhost:8080/ehrbase/rest/openehr/v1/ehr/8dcd91be-ccb2-4ace-8a18-88d9bd5bce5b/directory
Accept: application/json
```

```http
GET http://localhost:8080/ehrbase/rest/openehr/v1/ehr/8dcd91be-ccb2-4ace-8a18-88d9bd5bce5b/composition/a5b1e471-f28f-4365-b0b0-51c1fb03b112::local.ehrbase.org::1
Accept: application/json
```

**Cautions:** The `DV_EHR_URI` references were persisted and retrieved, but native full-URI dereferencing was not demonstrated. AQL-based targeted retrieval was demonstrated for selected blood pressure OBSERVATION and SOAP SECTION targets. The Basic FOLDER implementation does not store `Primary` or `Associated` relationship roles. All identifiers refer to the Basic FOLDER T1 EHR, not the T0 or exploratory extension EHRs.

**Related documentation:** [`DOC-03-poc-plan.md`](../../DOC-03-poc-plan.md) and [`DOC-04-poc-results.md`](../../DOC-04-poc-results.md) at the PoC root, and [`README.md`](README.md) for T1 test artifacts.
