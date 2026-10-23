# T2 LINK-Based Implementation: Design and Technical Behavior

Scope: Episode-oriented medical record proof of concept, T2 LINK pattern.  
Status: Implementation and relationship-retrieval tests completed, 19 October 2026.  
Repository location: `08-technical-proof-of-concept/04-link-pattern/T2/`.

## 1. Design objective

Assess a relationship representation based on openEHR Reference Model `LINK` instances, without changing the Reference Model or duplicating clinical content. The reference model distinguishes three contexts:

1. **Care Encounter** — the care-contact context, represented by a Care Encounter COMPOSITION with links to MR COMPOSITIONs documented during that contact.
2. **Episode of Care** — longitudinal health-problem context, represented by an Episode of Care COMPOSITION with links to individual clinical ENTRYs.
3. **Medical Record** — the clinical documentation, persisted as standard archetyped COMPOSITIONs containing the original ENTRYs.

The clinical relationship rules and CR identifiers are defined in [DOC-02](../../DOC-02-poc-clinical-relationships.md). T2 implements those rules without redefining them.

## 2. Architecture and reference direction

```text
EHR: dc1bb0c2-342f-4f6a-b426-65b63dffa9a0
│
├── Care Encounter COMPOSITIONs
│   ├── CE1 ── LINK(type=encounter) ──► MR1, MR2, MR3, MR4, MR5 COMPOSITIONs
│   └── CE2 ── LINK(type=encounter) ──► MR6, MR7, MR8, MR9 COMPOSITIONs
│
├── Episode of Care COMPOSITIONs
│   ├── EP1 ── 7 Primary LINKs ──► individual MR ENTRYs
│   ├── EP2 ── 12 Primary LINKs ──► individual MR ENTRYs
│   ├── EP3 ── 2 Associated LINKs ──► MR1/MR7 Blood Pressure ENTRYs
│   └── EP4 ── 3 Associated LINKs ──► MR2 Height/Weight/BMI ENTRYs
│
└── Medical Record COMPOSITIONs (MR1–MR9)
    └── 19 distinct clinical ENTRYs; clinical data stored only here
```

The reference direction is an implementation decision: CE and EP COMPOSITIONs contain LINK objects targeting MR content. The clinical specification's relationship wording does not imply that the `LINK` objects reside inside the MR ENTRYs.

EP1 is the default General Health Problem episode, not a parent in a hierarchy. Associated assignments to EP3/EP4 do not imply parent–child episode relationships.

## 3. LINK representation

### 3.1 Care Encounter → MR COMPOSITION

```json
{
  "meaning": {"_type": "DV_TEXT", "value": "documented by"},
  "type": {"_type": "DV_TEXT", "value": "encounter"},
  "target": {
    "_type": "DV_EHR_URI",
    "value": "ehr://dc1bb0c2-342f-4f6a-b426-65b63dffa9a0/5f73b7ab-3b72-4951-9c75-a8336c37b5ac::local.ehrbase.org::1"
  }
}
```

The target is the versioned MR COMPOSITION, not an individual ENTRY. CE1 contains five such LINKs, and CE2 contains four.

### 3.2 Episode of Care → clinical ENTRY

```json
{
  "meaning": {"_type": "DV_TEXT", "value": "is related to the same episode"},
  "type": {"_type": "DV_TEXT", "value": "episode-of-care-primary"},
  "target": {
    "_type": "DV_EHR_URI",
    "value": "ehr://dc1bb0c2-342f-4f6a-b426-65b63dffa9a0/5f73b7ab-3b72-4951-9c75-a8336c37b5ac::local.ehrbase.org::1/content%5BopenEHR-EHR-OBSERVATION.blood_pressure.v2%5D"
  }
}
```

For an Associated relationship, set `type.value` to `episode-of-care-associated` while retaining the same target URI. MR1 Blood Pressure is Primary in EP1 and Associated in EP3. Both LINKs target the same ENTRY.

The role labels (`episode-of-care-primary` and `episode-of-care-associated`) are conventions adopted in this PoC. Their clinical constraints are not automatically enforced by the tested repository.

### 3.3 URI encoding

ENTRY paths contain square brackets. In `DV_EHR_URI` targets, encode `[` as `%5B` and `]` as `%5D`, including at every level of a nested SOAP path. An initial smoke test with literal square brackets failed with HTTP 400. Encoded targets were persisted successfully.

### 3.4 Versioning

References contain the **versioned** target COMPOSITION UID, e.g. `::1`. This gives a precise reference to the tested target version. Automatic retargeting to subsequent MR versions was not tested. EP1 and EP3 were updated using PUT and had versions `::2` at the documented test end state. Those versions were used for the final relationship counts.

## 4. Clinical granularity and SOAP notes

The nine MR COMPOSITIONs contain 19 technical ENTRYs. The two SOAP notes (MR4 and MR8) are each a single clinical documentation unit, but the CKM-based template stores Subjective, Objective, Assessment and Plan as four separate `OBSERVATION.progress_note.v1` ENTRYs inside `SECTION.soap.v0`.

Example unencoded SOAP target paths:

```text
/content[openEHR-EHR-SECTION.soap.v0]/items[at0001]/items[openEHR-EHR-OBSERVATION.progress_note.v1]
/content[openEHR-EHR-SECTION.soap.v0]/items[at0002]/items[openEHR-EHR-OBSERVATION.progress_note.v1]
/content[openEHR-EHR-SECTION.soap.v0]/items[at0003]/items[openEHR-EHR-OBSERVATION.progress_note.v1]
/content[openEHR-EHR-SECTION.soap.v0]/items[at0004]/items[openEHR-EHR-OBSERVATION.progress_note.v1]
```

All four ENTRYs of MR4 and all four ENTRYs of MR8 are assigned EP2 Primary. This preserves the intended clinical unity in the test data but does not demonstrate repository-enforced atomic episode assignment for a SOAP note.

## 5. Relationship cardinalities

| Context | Clinical relationships | Stored LINK instances | Reason |
|---|---:|---:|---|
| Care Encounter → MR COMPOSITION | 9 | 9 | One per MR COMPOSITION |
| Episode of Care → clinical unit | 18 | 24 | Two SOAP units each expand from one clinical assignment to four ENTRY-level links |
| **Total** | **27** | **33** | |

Episode relationships comprise seven Primary in EP1, twelve Primary in EP2, two Associated in EP3, and three Associated in EP4. There are 19 distinct target ENTRY URIs and five additional Associated relationships.

## 6. Persistence and query workflow

1. Create EHR and persist MR1–MR9 as clinical COMPOSITIONs.
2. Persist CE1/CE2 with `LINK`s targeting the relevant versioned MR COMPOSITION UIDs.
3. Persist EP1–EP4 with `LINK`s targeting versioned MR COMPOSITION UIDs **plus** ENTRY-specific paths.
4. Query each CE/EP COMPOSITION using AQL `c/links` to verify the individual stored LINKs.
5. Query all EP COMPOSITIONs to obtain the relationship type and target URI across the EHR.
6. Derive dataset-level integrity checks by grouping the retrieved relationships by exact target URI.
7. For clinical content retrieval, interpret the target URI and issue a separate, archetype-specific AQL query. This was demonstrated for MR1 Blood Pressure.

### 6.1 Consolidated episode relationship query (executed)

```aql
SELECT
  c/uid/value AS episode_composition_uid,
  c/links/type/value AS relationship_type,
  c/links/target/value AS target_uri
FROM EHR e
CONTAINS COMPOSITION c[openEHR-EHR-COMPOSITION.problem_list.v2]
WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0'
  AND c/archetype_details/template_id/value = 'JPM_Episode_of_Care.v1'
```

Observed: 24 rows, four EP COMPOSITIONs, 19 Primary and five Associated, at `2026-10-19T06:59:06.997654752Z`.

### 6.2 Selective ENTRY reconstruction (executed)

```aql
SELECT bp AS entry
FROM EHR e
CONTAINS COMPOSITION c
CONTAINS OBSERVATION bp[openEHR-EHR-OBSERVATION.blood_pressure.v2]
WHERE e/ehr_id/value = 'dc1bb0c2-342f-4f6a-b426-65b63dffa9a0'
  AND c/uid/value = '5f73b7ab-3b72-4951-9c75-a8336c37b5ac::local.ehrbase.org::1'
```

Observed: one full Blood Pressure OBSERVATION (140/90 mmHg), excluding the Pulse ENTRY. This was an application-constructed AQL query, not automatic dereferencing of the `ehr://` URI.

### 6.3 T2.7 — Complete EP2 view reconstruction (executed)

T2.7a queried the EP2 COMPOSITION (`9f04a0d0-1eed-4688-9d19-04cf3f1d5210::local.ehrbase.org::1`) and returned 12 Primary `LINK` target URIs spanning MR3, MR4, MR5, MR6, MR8, and MR9. T2.7b executed six independent AQL retrievals for the corresponding clinical content (12 ENTRYs total): one urinalysis, four MR4 SOAP progress-note ENTRYs, one medication order, one microbiology result with nested culture/susceptibility CLUSTERs, four MR8 SOAP ENTRYs, and one subsequent medication order. All returned the expected clinical structures and values.

T2.7c manually assembled the results into a chronological EP2 view covering CE1 (15 November 2024) and CE2 (17 November 2024), including suspected cystitis, initial antibiotic therapy, culture results and subsequent treatment change. This demonstrates feasibility on the tested dataset, not an automated end-to-end resolver. Reproducible query bodies and observed timestamps are recorded in [T2-link-test-identifiers.md](T2-link-test-identifiers.md).

## 7. Verification and limitations

| Capability | Observed result | Evidence boundary |
|---|---|---|
| Persist `LINK` objects on CE and EP COMPOSITIONs | PASS | 33 stored links |
| Query LINK objects and target URIs via AQL | PASS | 9 encounter + 24 episode links |
| Consolidate all episode links in one AQL result | PASS | 24 result rows |
| Validate one Primary relationship per referenced ENTRY | PASS | Derived from 24 returned links; not server enforcement |
| Assign one ENTRY to Primary and Associated episodes | PASS | Five repeated target URIs; no duplicated clinical ENTRY content |
| Preserve SOAP clinical unity in assignment data | PASS | Four links per SOAP note, all EP2 Primary |
| Select a clinical ENTRY using a separate AQL query | PASS | MR1 Blood Pressure |
| Native `DV_EHR_URI` resolution | Not demonstrated | No direct URI-resolver test succeeded |
| `GET .../composition/{uid}?path=...` filtering | Not demonstrated | Returned whole MR1 COMPOSITION, including BP and Pulse |
| Automatic primary uniqueness, SOAP consistency, dangling-link detection | Not tested | Application-level rules |
| Automatic reference updates after new target versions | Not tested | Version-specific targets |
| EP2 relationship resolution and retrieval of all 12 linked ENTRYs | PASS | T2.7a–b: six MR COMPOSITIONs, 12 ENTRYs, separate AQL requests |
| Chronological episode-oriented clinical view | PASS — manual assembly | T2.7c: reconstructed EP2 from retrieved clinical results |
| Automated URI traversal and clinical view assembly | Not implemented or tested | Requires application-side URI parsing, queries, grouping and ordering |

The experiment uses one synthetic EHR in EHRbase 2.30.1. The observed behavior must not be generalized to all openEHR CDRs without further testing.

## 8. Reproducibility and repository integration

[T2-link-test-identifiers.md](T2-link-test-identifiers.md) is the canonical identifier register and verification log for this T2 implementation. It records the tested versioned COMPOSITION UIDs, CR-001–CR-027 mapping, HTTP/AQL evidence, timestamps, expected and observed row counts, and negative findings. There is no separate `T2-link-identifiers.md` file in the documented T2 Markdown documentation set. Retain the versioned identifiers in the verification log to preserve the tested state even if repository content changes later.

The JSON bodies used for CE/EP POST and PUT operations should be retained alongside or linked from the documentation when available. This document does not claim that all Postman requests or response payloads have been committed to the repository.

## 9. Evaluation summary

T2.7 demonstrated EP2 relationship resolution (12 LINK targets), selective retrieval of all 12 ENTRYs from six MR COMPOSITIONs, and manual chronological assembly of the complete EP2 clinical view. An automated application that traverses LINK URIs, retrieves each ENTRY, and assembles the view was not implemented or tested.

The T2 PoC demonstrates a feasible LINK-based representation of longitudinal episode associations and care-encounter context without duplication of the 19 clinical ENTRYs. Its strengths are explicit reference relationships and the ability to query relationship metadata. Its observed implementation burden is the need to manage versioned ENTRY paths and to implement application-side resolution, integrity checks and consistency rules. The test does not establish native URI dereferencing or repository-enforced episode relationship constraints.

## Archived JSON evidence

The [`json/requests/`](json/requests/) directory contains the ten original POST/PUT request bodies, including preliminary smoke tests and a negative URI-encoding test. They document submitted payloads, not necessarily the resulting COMPOSITION versions. The [`json/persisted/`](json/persisted/) directory contains the fifteen JSON COMPOSITIONs retrieved from EHRbase (MR1–MR9, CE1–CE2 and EP1–EP4) with explicit versioned UIDs. These exports represent the validated T2 end state. See the [T2 README](README.md) for an artifact inventory and reproducibility qualifications.

Do not edit exported COMPOSITION JSON to align its `uid` with an earlier PUT request. The original request and the returned persisted version document different stages of versioned persistence.
