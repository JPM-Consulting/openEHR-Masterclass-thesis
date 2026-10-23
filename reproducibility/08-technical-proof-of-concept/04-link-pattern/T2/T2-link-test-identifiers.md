# T2 LINK Pattern: Test Identifiers and Verification Log

**Status:** T2 relationship persistence and AQL retrieval passed within the documented test scope. Native LINK-target dereferencing was not demonstrated.  
**Environment:** EHRbase 2.30.1, openEHR REST API, Postman, and local system `local.ehrbase.org`.  
**EHR ID:** `dc1bb0c2-342f-4f6a-b426-65b63dffa9a0`  
**Reference specification:** [DOC-02](../../DOC-02-poc-clinical-relationships.md) (CR-001–CR-027).  
**Scope:** T2 LINK-based pattern only. These identifiers must not be mixed with those of the T1 FOLDER EHR.

## 1. Versioned COMPOSITION identifiers

| ID | Content | Documented final versioned COMPOSITION UID |
|---|---|---|
| MR1 | Vital Signs, CE1 | `5f73b7ab-3b72-4951-9c75-a8336c37b5ac::local.ehrbase.org::1` |
| MR2 | Body Measurements, CE1 | `7e606fc5-6a49-4c97-ab52-4167f045c6d7::local.ehrbase.org::1` |
| MR3 | Urinalysis, CE1 | `3c02c656-c63d-4944-b06d-c32c7e2ddcf8::local.ehrbase.org::1` |
| MR4 | SOAP Progress Note, CE1 | `cbe82162-bacc-41a5-a252-575fb5bafbbd::local.ehrbase.org::1` |
| MR5 | Medication Order, CE1 | `c1c90004-961b-4a09-9ed3-c67cde8027fb::local.ehrbase.org::1` |
| MR6 | Microbiology Result, CE2 | `bd64397e-9a0b-4fc1-af59-720c3d7f0eaa::local.ehrbase.org::1` |
| MR7 | Vital Signs, CE2 | `22b21098-90d0-4c56-9ba1-0244436a6ee0::local.ehrbase.org::1` |
| MR8 | SOAP Progress Note, CE2 | `1a226cc5-7f59-45f9-9833-42d976d3c63c::local.ehrbase.org::1` |
| MR9 | Medication Order, CE2 | `71c9f21b-9165-4fb4-9fa2-343486fcf37a::local.ehrbase.org::1` |
| CE1 | Care Encounter 1 | `677552a4-fd78-4678-b91c-0172bc118017::local.ehrbase.org::2` |
| CE2 | Care Encounter 2 | `4805a3a9-7518-4bd8-9f5f-e57bcfcb30c2::local.ehrbase.org::1` |
| EP1 | General Health Problem (default, **not** parent) | `6e963022-99a0-45ff-803b-24b835f254ce::local.ehrbase.org::2` |
| EP2 | Urinary Tract Infection | `9f04a0d0-1eed-4688-9d19-04cf3f1d5210::local.ehrbase.org::1` |
| EP3 | Arterial Hypertension | `e7aaa7a9-c8d9-4533-8725-9c51d4d7e003::local.ehrbase.org::2` |
| EP4 | Obesity WHO grade I | `81bcb7b2-7db7-480c-abcd-9c5441e51f73::local.ehrbase.org::1` |

**Versioning caveat:** EP1 `::1` contained one LINK and EP1 `::2` contained seven. EP3 `::1` contained one LINK and EP3 `::2` contained two. Query the relevant persisted version explicitly when verifying the documented final counts.

## 2. Clinical relationship register and technical expansion

`DOC-02` specifies **27 clinical relationships**: nine CE assignments (CR-001–CR-009) and 18 episode assignments (CR-010–CR-027). Two SOAP clinical relationships (CR-020 and CR-026) each expand to four ENTRY references, yielding **33 persisted LINKs**: 9 CE → COMPOSITION and 24 EP → ENTRY (19 Primary, 5 Associated).

| CR ID | Source clinical unit | Clinical target | Role | Stored technical LINK count |
|---|---|---|---|---:|
| CR-001–CR-005 | MR1–MR5 | CE1 | belongs to | 5 |
| CR-006–CR-009 | MR6–MR9 | CE2 | belongs to | 4 |
| CR-010 | MR1 Blood Pressure | EP1 | Primary | 1 |
| CR-011 | MR1 Blood Pressure | EP3 | Associated | 1 |
| CR-012 | MR1 Pulse | EP1 | Primary | 1 |
| CR-013 | MR2 Height | EP1 | Primary | 1 |
| CR-014 | MR2 Height | EP4 | Associated | 1 |
| CR-015 | MR2 Weight | EP1 | Primary | 1 |
| CR-016 | MR2 Weight | EP4 | Associated | 1 |
| CR-017 | MR2 BMI | EP1 | Primary | 1 |
| CR-018 | MR2 BMI | EP4 | Associated | 1 |
| CR-019 | MR3 Urinalysis | EP2 | Primary | 1 |
| CR-020 | MR4 SOAP (S/O/A/P) | EP2 | Primary | **4** |
| CR-021 | MR5 Medication Order | EP2 | Primary | 1 |
| CR-022 | MR6 Microbiology Result | EP2 | Primary | 1 |
| CR-023 | MR7 Blood Pressure | EP1 | Primary | 1 |
| CR-024 | MR7 Blood Pressure | EP3 | Associated | 1 |
| CR-025 | MR7 Pulse | EP1 | Primary | 1 |
| CR-026 | MR8 SOAP (S/O/A/P) | EP2 | Primary | **4** |
| CR-027 | MR9 Medication Order | EP2 | Primary | 1 |

**Reference direction in T2:** CE COMPOSITIONs contain LINKs to whole MR COMPOSITIONs (`type=encounter`, `meaning=documented by`); EP COMPOSITIONs contain LINKs to individual MR ENTRY paths (`type=episode-of-care-primary` or `episode-of-care-associated`, `meaning=is related to the same episode`). This direction is a T2 implementation choice, not the clinical source/target direction in DOC-02.

## 3. Persisted LINK counts and evidence

| Source | Documented version | LINKs | Type | Individual AQL validation (UTC) | Result |
|---|---|---:|---|---|---|
| CE1 | `::2` | 5 | encounter | 2026-10-19 05:49:09.366956336 | PASS |
| CE2 | `::1` | 4 | encounter | 2026-10-19 05:55:41.851374046 | PASS |
| EP1 | `::2` | 7 | Primary | 2026-10-19 06:41:31.031387763 | PASS |
| EP2 | `::1` | 12 | Primary | 2026-10-19 06:46:53.000832718 | PASS |
| EP3 | `::2` | 2 | Associated | 2026-10-19 06:54:58.52436947 | PASS |
| EP4 | `::1` | 3 | Associated | 2026-10-19 06:58:12.801053046 | PASS |
| **Total** | | **33** | **9 CE + 19 Primary + 5 Associated** | | **PASS** |

**Consolidated EP AQL:** Executed at 2026-10-19 06:59:06.997654752 UTC. The response contained `meta.resultsize=24`, four EP COMPOSITION UIDs, 19 Primary and five Associated relationships, 19 distinct target ENTRY URIs, and nine target MR COMPOSITION UIDs. PASS. Individual AQL `c/links` projections return **one row per LINK**, not one row containing an array.

## 4. Reproducible Postman/AQL requests

**Endpoint:** `POST http://localhost:8080/ehrbase/rest/openehr/v1/query/aql`  
**Headers:** `Content-Type: application/json` and `Accept: application/json`.

### 4.1 CE1 and CE2 — individual checks

```json
{"q":"SELECT c/uid/value AS composition_uid, c/links AS links FROM EHR e CONTAINS COMPOSITION c WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0' AND c/uid/value = '677552a4-fd78-4678-b91c-0172bc118017::local.ehrbase.org::2'"}
```

CE1 expected `resultsize=5`. For CE2, substitute `4805a3a9-7518-4bd8-9f5f-e57bcfcb30c2::local.ehrbase.org::1`; expected `resultsize=4`.

### 4.2 EP1–EP4 — individual checks

```json
{"q":"SELECT c/uid/value AS composition_uid, c/links AS links FROM EHR e CONTAINS COMPOSITION c WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0' AND c/uid/value = '81bcb7b2-7db7-480c-abcd-9c5441e51f73::local.ehrbase.org::1'"}
```

EP4 expected `resultsize=3`. Substitute each documented final EP UID from section 1 for the other episodes; expected EP1=7, EP2=12, EP3=2.

### 4.3 T2.6a — consolidated episode relationship query (executed, PASS)

```json
{
  "q": "SELECT c/uid/value AS episode_composition_uid, c/links/type/value AS relationship_type, c/links/target/value AS target_uri FROM EHR e CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.problem_list.v2] WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0' AND c/archetype_details/template_id/value = 'JPM_Episode_of_Care.v1'"
}
```

**Observed:** `resultsize=24` with columns `episode_composition_uid`, `relationship_type`, and `target_uri`. The results comprised seven EP1 Primary, twelve EP2 Primary, two EP3 Associated, and three EP4 Associated relationships. The returned `target_uri` values are versioned `ehr://` URIs with percent-encoded brackets `%5B`/`%5D`.

### 4.4 T2.4h.2 — selective clinical ENTRY reconstruction via AQL (executed, PASS)

```json
{
  "q": "SELECT bp AS entry FROM EHR e CONTAINS COMPOSITION c CONTAINS OBSERVATION bp[openEHR-EHR-OBSERVATION.blood_pressure.v2] WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0' AND c/uid/value = '5f73b7ab-3b72-4951-9c75-a8336c37b5ac::local.ehrbase.org::1'"
}
```

**Observed:** At 2026-10-19 06:26:07.968699127 UTC, `resultsize=1`. The MR1 Blood Pressure OBSERVATION (140/90 mmHg) was returned without MR1 Pulse. This is an **application-driven AQL selection**, not native resolution of a `DV_EHR_URI` target.

### 4.5 MR4 SOAP — four technical ENTRYs, one clinical note (executed, PASS)

```json
{
  "q": "SELECT s/items[at0001]/items[openEHR-EHR-OBSERVATION.progress_note.v1] AS subjective, s/items[at0002]/items[openEHR-EHR-OBSERVATION.progress_note.v1] AS objective, s/items[at0003]/items[openEHR-EHR-OBSERVATION.progress_note.v1] AS assessment, s/items[at0004]/items[openEHR-EHR-OBSERVATION.progress_note.v1] AS plan FROM EHR e CONTAINS COMPOSITION c CONTAINS SECTION s[openEHR-EHR-SECTION.soap.v0] WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0' AND c/uid/value = 'cbe82162-bacc-41a5-a252-575fb5bafbbd::local.ehrbase.org::1'"
}
```

**Observed:** At 2026-10-19 06:31:19.958393175 UTC, the response contained one result row with four distinct ENTRY columns. The four MR4 ENTRYs and four MR8 ENTRYs all reference EP2 Primary. The same SOAP AQL query was **not independently run for MR8** in this test log; MR8 content was inspected via GET.

## 5. Referential paths and URI encoding

**CE LINK target:** `ehr://<ehr_id>/<versioned MR COMPOSITION UID>`.

**EP LINK target:** `ehr://<ehr_id>/<versioned MR COMPOSITION UID>/<ENTRY path>`.

Example MR1 Blood Pressure (EP1 Primary and EP3 Associated point to the **same URI**):

```text
ehr://dc1bb0c2-342f-4f6a-b426-65b63dffa9a0/5f73b7ab-3b72-4951-9c75-a8336c37b5ac::local.ehrbase.org::1/content%5BopenEHR-EHR-OBSERVATION.blood_pressure.v2%5D
```

SOAP ENTRY paths, before URI encoding:

```text
/content[openEHR-EHR-SECTION.soap.v0]/items[at0001]/items[openEHR-EHR-OBSERVATION.progress_note.v1]
/content[openEHR-EHR-SECTION.soap.v0]/items[at0002]/items[openEHR-EHR-OBSERVATION.progress_note.v1]
/content[openEHR-EHR-SECTION.soap.v0]/items[at0003]/items[openEHR-EHR-OBSERVATION.progress_note.v1]
/content[openEHR-EHR-SECTION.soap.v0]/items[at0004]/items[openEHR-EHR-OBSERVATION.progress_note.v1]
```

**Negative finding:** Raw `[` and `]` inside `DV_EHR_URI` caused HTTP 400 in the initial smoke test. Encoding the brackets as `%5B` and `%5D` permitted persistence and AQL retrieval. The stored SOAP targets contain encoded brackets at each path segment.

## 6. Integrity checks: T2.6b (derived from T2.6a response)

- 19 distinct target ENTRY URIs, each with **exactly one** `episode-of-care-primary` relationship.
- Five of those ENTRY URIs additionally have **one** `episode-of-care-associated` relationship: MR1 BP → EP3; MR7 BP → EP3; MR2 Height, Weight and BMI → EP4.
- No primary-less, multiply-primary, or duplicate episode–ENTRY pairs in the **24 returned relationships**.
- MR4 and MR8 SOAP notes: four distinct progress-note ENTRY targets per note, all EP2 Primary. Clinical unity is an application-level invariant. EHRbase enforcement was not tested.
- Scope caveat: these checks validate the returned LINK dataset, not an exhaustive independent inventory of all ENTRYs in the repository, nor automatic referential integrity.

## 7. Limitations and negative findings

1. **No native LINK dereferencing demonstrated.** T2.4h.1 `GET /ehr/{ehr_id}/composition/{mr1_uid}?path=/content%5BopenEHR-EHR-OBSERVATION.blood_pressure.v2%5D` returned HTTP 200 with the **whole MR1 COMPOSITION** (BP **and** Pulse). This did not establish ENTRY filtering by the `path` parameter. It does not prove dereferencing is generally unsupported.
2. **AQL reconstructs a selected ENTRY**, but the application must interpret the target URI, determine the MR COMPOSITION and ENTRY archetype/path, and formulate the appropriate query. No automatic `ehr://` resolution was exercised.
3. **No repository-enforced relationship constraints demonstrated.** Primary uniqueness, SOAP unity, role semantics and absence of dangling targets require explicit validation or application logic; this dataset satisfies them, but server-side enforcement was not tested.
4. **Version-sensitive references.** LINK targets point to specific versioned MR COMPOSITIONs; behaviour after subsequent target updates was not tested.
5. **Scope:** One synthetic patient, one EHR, nine MRs, two encounters, and four episodes. Findings are implementation-specific and do not imply universal support across openEHR CDRs.

## 8. Local JSON artefacts used

| Artefact | Purpose |
|---|---|
| `T2.3a-CE1-PUT-links-MR1-MR5.json` | CE1 five encounter LINKs |
| `T2.3c-CE2-POST-links-MR6-MR9.json` | CE2 four encounter LINKs |
| `T2_EP1_PUT_v2.json` | EP1 seven Primary LINKs |
| `T2_EP2_POST_12_links.json` | EP2 twelve Primary LINKs |
| `T2_EP3_PUT_2_associated_links.json` | EP3 two Associated LINKs |
| `T2_EP4_POST_3_associated_links.json` | EP4 three Associated LINKs |
| [DOC-02](../../DOC-02-poc-clinical-relationships.md) | Authoritative clinical relationship register |

## 9. Test conclusion

T2 relationship persistence, retrieval, and dataset-level role consistency: PASS. The 27 implementation-independent clinical relationships were represented by 33 persisted LINK instances (9 encounter COMPOSITION targets and 24 episode ENTRY targets), and all 33 were retrieved through AQL. The episode links cover 19 distinct clinical ENTRYs with exactly one Primary relationship each and five additional Associated relationships. Native dereferencing, enforcement of relationship invariants and update propagation remain **unverified** and must not be reported as demonstrated capabilities.


## 10. T2.7 — Episode-of-Care clinical view reconstruction (19 October 2026)

**Episode:** EP2, Urinary Tract Infection. **Versioned EP COMPOSITION UID:** `9f04a0d0-1eed-4688-9d19-04cf3f1d5210::local.ehrbase.org::1`.

### 10.1 T2.7a — Resolve EP2 relationship targets (PASS)

AQL request (POST `/ehrbase/rest/openehr/v1/query/aql`):

```json
{"q":"SELECT c/uid/value AS episode_composition_uid, c/links/type/value AS relationship_type, c/links/target/value AS target_uri FROM EHR e CONTAINS COMPOSITION c WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0' AND c/uid/value = '9f04a0d0-1eed-4688-9d19-04cf3f1d5210::local.ehrbase.org::1'"}
```

**Observed:** At `2026-10-19T07:16:49.730696222Z`, `resultsize=12`. All relationships were `episode-of-care-primary`, covering six distinct MR COMPOSITION UIDs and 12 distinct ENTRY target URIs. MR4 and MR8 each contribute four SOAP ENTRY paths. **PASS**.

### 10.2 T2.7b — Retrieve all linked clinical ENTRYs (PASS)

All queries below use `POST /ehrbase/rest/openehr/v1/query/aql` with JSON body `{"q":"<AQL>"}`. Each returned `resultsize=1`. For SOAP notes, one row contains four distinct `OBSERVATION.progress_note.v1` columns, not one ENTRY.

| Test | MR | ENTRY type and count | Observed result timestamp (UTC) | Result |
|---|---|---:|---|---|
| T2.7b.1 | MR3 | Urinalysis OBSERVATION × 1 | `2026-10-19T07:17:34.481537548Z` | PASS: leukocytes 3+, nitrite Positive, blood 1+, protein Trace, pH 6.0 |
| T2.7b.2 | MR4 | SOAP progress-note OBSERVATION × 4 | `2026-10-19T07:18:06.511822341Z` | PASS: S/O/A/P; suspected cystitis |
| T2.7b.3 | MR5 | Medication-order INSTRUCTION × 1 | `2026-10-19T07:18:39.34452055Z` | PASS: TMP 160 mg / SMX 800 mg, PO 2×1, 12 h interval |
| T2.7b.4 | MR6 | Laboratory-result OBSERVATION × 1 | `2026-10-19T07:19:07.689170008Z` | PASS: urine culture, *E. coli*, five antimicrobial susceptibility results, nested CLUSTER |
| T2.7b.5 | MR8 | SOAP progress-note OBSERVATION × 4 | `2026-10-19T07:19:47.701242179Z` | PASS: S/O/A/P; acute bacterial cystitis and therapy change |
| T2.7b.6 | MR9 | Medication-order INSTRUCTION × 1 | `2026-10-19T07:20:12.737457844Z` | PASS: amoxicillin 500 mg / clavulanate 125 mg, PO 3×1, 8 h interval |
| **Total** | **6 MR** | **12 ENTRYs** | | **PASS** |

#### Executed AQL requests for T2.7b

**MR3:**
```aql
SELECT u AS entry FROM EHR e CONTAINS COMPOSITION c CONTAINS OBSERVATION u[openEHR-EHR-OBSERVATION.urinalysis.v1] WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0' AND c/uid/value = '3c02c656-c63d-4944-b06d-c32c7e2ddcf8::local.ehrbase.org::1'
```

**MR4 and MR8 (execute separately with the appropriate versioned COMPOSITION UID):**
```aql
SELECT s/items[at0001]/items[openEHR-EHR-OBSERVATION.progress_note.v1] AS subjective, s/items[at0002]/items[openEHR-EHR-OBSERVATION.progress_note.v1] AS objective, s/items[at0003]/items[openEHR-EHR-OBSERVATION.progress_note.v1] AS assessment, s/items[at0004]/items[openEHR-EHR-OBSERVATION.progress_note.v1] AS plan FROM EHR e CONTAINS COMPOSITION c CONTAINS SECTION s[openEHR-EHR-SECTION.soap.v0] WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0' AND c/uid/value = 'cbe82162-bacc-41a5-a252-575fb5bafbbd::local.ehrbase.org::1'
```
MR8 UID to substitute: `1a226cc5-7f59-45f9-9833-42d976d3c63c::local.ehrbase.org::1`.

**MR5 and MR9 (execute separately with the appropriate versioned COMPOSITION UID):**
```aql
SELECT m AS entry FROM EHR e CONTAINS COMPOSITION c CONTAINS INSTRUCTION m[openEHR-EHR-INSTRUCTION.medication_order.v3] WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0' AND c/uid/value = 'c1c90004-961b-4a09-9ed3-c67cde8027fb::local.ehrbase.org::1'
```
MR9 UID to substitute: `71c9f21b-9165-4fb4-9fa2-343486fcf37a::local.ehrbase.org::1`.

**MR6:**
```aql
SELECT lab AS entry FROM EHR e CONTAINS COMPOSITION c CONTAINS OBSERVATION lab[openEHR-EHR-OBSERVATION.laboratory_test_result.v1] WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0' AND c/uid/value = 'bd64397e-9a0b-4fc1-af59-720c3d7f0eaa::local.ehrbase.org::1'
```

### 10.3 T2.7c — Assemble a chronological EP2 clinical view (PASS, manual)

| Encounter | Date/time | MR | Reconstructed content |
|---|---|---|---|
| CE1 | 2024-11-15 09:00 +01:00 | MR3 | Urinalysis: leukocytes 3+, nitrite Positive, blood 1+, protein Trace, pH 6.0 |
| CE1 | 2024-11-15 09:00 +01:00 | MR4 | SOAP: S burning urination for three days; O pyuria; A suspected cystitis; P antibiogram requested, empirical TMP-SMX |
| CE1 | 2024-11-15 09:00 +01:00 | MR5 | TMP-SMX (TMP 160 mg / SMX 800 mg), oral, twice daily |
| CE2 | 2024-11-17 09:00 +01:00 | MR6 | Urine culture ≥10⁵ CFU/mL, *E. coli*: resistant to TMP-SMX and ciprofloxacin; sensitive to amoxicillin–clavulanate, nitrofurantoin and fosfomycin |
| CE2 | 2024-11-17 09:00 +01:00 | MR8 | SOAP: S persistent urinary symptoms; O culture resistant to current antibiotic; A acute bacterial cystitis; P switch antimicrobial therapy |
| CE2 | 2024-11-17 09:00 +01:00 | MR9 | Amoxicillin 500 mg / clavulanate 125 mg, oral, three times daily |

**Result:** The 12 linked ENTRYs were retrieved from six original MR COMPOSITIONs and manually combined into a chronological EP2 clinical view spanning two encounters, without creating duplicate clinical ENTRYs. The underlying relationship retrieval and content queries were executed successfully; **no software implementation of automated LINK URI traversal, dereferencing or view assembly was tested**. This is a manual proof of feasibility for the defined synthetic dataset, not a demonstration of an automatic EHRbase episode-view feature.

**Status update:** Sections 1–9 document earlier T2 tests. Section 10 adds the subsequent T2.7 test. Native dereferencing, repository-enforced relationship constraints, and version-update propagation remain unverified.

## 11. Archived JSON evidence and consolidation

Fifteen final COMPOSITION versions are archived under `json/persisted/`: nine MR COMPOSITIONs (MR1–MR9), two CE COMPOSITIONs, and four EP COMPOSITIONs. The six CE/EP exports contain **33 LINKs** (9 encounter, 19 primary episode, 5 associated episode). The 10 request bodies are retained separately under `json/requests/`, including the failed unencoded-URI smoke test.

The exported COMPOSITION UIDs were compared against the canonical identifier register in section 1. The 15 archived exports matched, and all JSON documents parsed successfully. The original JSON bytes were preserved during consolidation. MR9 is included in the current archive as `T2-MR9-final.json`.

This is an **offline consistency check of archived artefacts**, not an additional live REST or AQL test. For reproducibility, distinguish submitted PUT bodies containing prior-version identifiers from the subsequently persisted versions. No native LINK URI dereferencing or automated EP2 clinical-view assembly was demonstrated.
