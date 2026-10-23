# T4: Execution and Verification Log

Scenario: T4 (CLUSTER, Medical Records first). EHR: `3c269710-a677-4fe8-9083-1133e8899db9`. Environment: EHRbase 2.30.1, REST canonical JSON, AQL and Postman. Overall result: PASS within the documented test scope.

## Test Phases

| Phase | Test | Observed evidence | Status |
|---|---|---|---|
| T4.1 | Create EHR | POST 201 and GET EHR 200 | PASS |
| T4.2 | Persist MR1–MR9 | Nine POST 201 and nine independent GET 200. No relationship CLUSTERs in MRs | PASS |
| T4.3 | CE1 POST/GET | POST 201 and GET 200. Five CE→MR URI references | PASS |
| T4.4 | CE2 POST without refs | POST 201 and GET 200 for `::1`. Relationship CLUSTER absent | PASS |
| T4.5 | CE2 PUT with refs | PUT 200. GET `::2` 200 with four references and GET historical `::1` 200 without references | PASS |
| T4.6 | EP1–EP4 POST/GET | Four POST 201 and independent GET 200. 7 + 12 + 2 + 3 = 24 EP→ENTRY references | PASS |
| T4.7 | REST / AQL inventory | EHR GET 200. AQL returned 15 current COMPOSITIONs (9 MR + 2 CE + 4 EP) | PASS |
| T4.8 | Relationship AQL | 9 CE→MR URI rows and 24 EP→ENTRY URI rows, totaling 33 | PASS |
| T4.9 | Clinical view reconstruction | 19 clinical MR ENTRYs, 12 EP2 references, MR3 urinalysis, MR4/MR8 SOAP sections, and 4 diagnoses | PASS for tested views |
| T4.10 | Documentation | Report, identifiers, queries, request checksums, and 16 persisted COMPOSITION JSON exports documented | DOCUMENTED |

## Reference-Level Findings

- CE1 contains five references to MR1–MR5. CE2 `::2` contains four references to MR6–MR9. The earlier CE2 `::1` remains retrievable and contains no relationship CLUSTER.
- EP1 has seven Primary references, EP2 has twelve Primary references, EP3 has two Associated references, and EP4 has three Associated references. EP2 covers six MR COMPOSITIONs across two encounters.
- The initial EP1 POST with unencoded `[` and `]` in URI paths returned HTTP 400. The URI-encoded correction returned HTTP 201. Both request variants are retained and labelled.

## Clinical Reconstruction

| Query / view | Observed result | Status |
|---|---|---|
| All ENTRY inventory | 25 ENTRYs = 19 clinical MR ENTRYs + 2 CE EVALUATIONs + 4 EP EVALUATIONs | PASS |
| Clinical MR-only inventory | 19 ENTRYs across nine MR COMPOSITIONs (11 on 15 Nov, 8 on 17 Nov) | PASS |
| EP2 relationship filter | 12 Primary URI references across MR3, MR4, MR5, MR6, MR8, MR9 | PASS |
| MR3 full urinalysis | Leukocytes 3+, nitrite Positive, blood 1+, protein Trace, pH 6.0 | PASS |
| MR4 SOAP SECTION | One `SECTION.soap.v0`, four leaf sections S/O/A/P, four progress-note OBSERVATIONs | PASS |
| MR8 SOAP SECTION | One `SECTION.soap.v0`, four leaf sections S/O/A/P, four progress-note OBSERVATIONs | PASS |
| Longitudinal EP2 SOAP narrative | 15 Nov suspected cystitis and empirical TMP–SMX, followed by 17 Nov persistent symptoms, resistant E. coli, and a treatment change | PASS within tested view |
| Diagnosis/problem list | Four EP diagnoses with `Current` and `Active` qualifiers | PASS |

### Diagnosis AQL Path Correction

The first diagnosis query used `d/data/items[at0001]/value/value` and returned four null values: `at0001` is the `ITEM_TREE`, not the diagnosis ELEMENT. Inspecting the full EP2 `EVALUATION.problem_diagnosis.v1` established the correct path `d/data/items[at0002]/value/value`. The corrected four-episode query returned General health problem, Urinary tract infection, Arterial hypertension (Dx 2009), and Obesity WHO grade I. All were `Current` / `Active`.

### SOAP Clinical Unity

Both MR4 and MR8 returned exactly one `SECTION.soap.v0`, each with four nested leaf sections (`at0001` Subjective, `at0002` Objective, `at0003` Assessment, `at0004` Plan) and one `OBSERVATION.progress_note.v1` per leaf. This documents the SOAP section structure and supports treating each SOAP note as one clinical unit despite four technical ENTRY references per note. No server-enforced all-or-none episode assignment was tested.

## Archived Persistence and Versioning Evidence

- `json/persisted/`: 16 JSON response bodies representing 15 logical COMPOSITIONs: 9 MR, 2 CE, 4 EP current versions and CE2 historical version `::1`. The historical version has no relationship CLUSTER. Current CE2 `::2` contains four MR references.
- Offline validation of the uploaded JSON bodies confirms 33 `DV_EHR_URI` values (CE1 5, CE2 `::2` 4, EP1–EP4 24). The evidence manifest lists exact filenames, versioned UIDs and SHA-256 hashes.
- The original ZIP filename `T4-M5-final.json` for MR5 is retained in the manifest. An optional filename-only correction to `T4-MR5-final.json` would not change the JSON content.

## Evidence and Interpretation Boundaries

- The user supplied eight JSON request bodies and 16 separately archived persisted COMPOSITION GET response bodies (15 current versions plus historical CE2 `::1`). All 16 JSON files were parsed and checked against the expected versioned UIDs. The 33 stored `DV_EHR_URI` values were counted. Original HTTP status/header logs and raw AQL response exports were not supplied. Do not conflate request payloads with persisted GET exports.
- AQL returned stored URI strings. The test did not demonstrate native target dereferencing or validate target existence using a URI resolver.
- No repository-enforced relationship mandatory constraints, referential integrity, primary uniqueness, historical-reference resolution, concurrency, performance, or full eight-user-story/six-criterion evaluation was demonstrated.
- AQL clinical MR-only filter in the test used COMPOSITION display names. A production implementation should use more robust template/archetype classification.

## Conclusion

T4 supports the technical feasibility of CE/EP-held CLUSTER references with Medical Record-first persistence, historical CE version retention, queryable context relationships and application-level clinical view reconstruction without clinical MR duplication. The result does not establish automatic relationship semantics or their enforcement by the CDR.
