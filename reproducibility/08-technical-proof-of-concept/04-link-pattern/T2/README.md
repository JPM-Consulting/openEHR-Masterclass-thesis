# T2: LINK-Based Episode-of-Care Pattern

Status: Implemented and verified within the documented synthetic PoC test scope (October 19, 2026).  
Environment: EHRbase 2.30.1, openEHR REST API, AQL, Postman.  
EHR: `dc1bb0c2-342f-4f6a-b426-65b63dffa9a0`.

## Purpose and scope

T2 evaluates whether standard openEHR `LINK` objects can represent episode-oriented and encounter-oriented relationships while retaining clinical content in its original Medical Record (MR) COMPOSITIONs. The pattern is compared with the FOLDER and CLUSTER implementation patterns. This directory documents T2 only.

The reference scenario has nine MR COMPOSITIONs (MR1–MR9), two Care Encounters (CE1–CE2), and four Episodes of Care (EP1–EP4). The implementation-independent clinical relationships are specified in [DOC-02](../../DOC-02-poc-clinical-relationships.md) (CR-001–CR-027).

## Documentation map

| File | Purpose |
|---|---|
| `README.md` | Entry point, scope, results and navigation (this file). |
| [`T2-link-implementation.md`](T2-link-implementation.md) | Architecture, relationship semantics, representation, versioning and reconstruction. |
| [`T2-link-test-identifiers.md`](T2-link-test-identifiers.md) | Authoritative T2 identifier register and reproducible verification log: versioned UIDs, CR mapping, AQL, evidence and limitations. |

## JSON artifacts and repository layout

| Location | Contents | Interpretation |
|---|---|---|
| [`json/requests/`](json/requests/) | 10 original POST/PUT JSON request bodies, ordered by T2 test IDs | Includes exploratory smoke tests, a failed unencoded URI test, and subsequent successful requests. These are not final COMPOSITION exports. |
| [`json/persisted/`](json/persisted/) | 15 GET-exported JSON COMPOSITIONs: MR1–MR9, CE1–CE2, EP1–EP4 | Evidence of the persisted final versions, including 9 encounter and 24 episode LINKs in CE/EP exports. |

Archive completeness: `T2-MR9-final.json` is present. All 15 final COMPOSITION exports are archived.

The source archive was consolidated by correcting `persited/` to `persisted/`, renaming `T2-Ep2-final.json` to `T2-EP2-final.json`, and excluding macOS metadata. Clinical JSON contents were not modified. T2 and T3 are separate test implementations under the common LINK-pattern directory.

Reproducibility qualification: The JSON exports contain EHR-specific and version-specific identifiers. Replaying the original requests in a newly created EHR requires appropriate UID and LINK-target remapping and correct POST/PUT sequencing. The files document the executed PoC and do not constitute an automated installation script.

## Implementation summary

- 9 MR COMPOSITIONs store the clinical data (19 distinct clinical ENTRYs).
- 2 Care Encounter COMPOSITIONs store 9 LINKs targeting whole MR COMPOSITIONs.
- 4 Episode of Care COMPOSITIONs store 24 LINKs targeting specific MR ENTRY paths: 19 Primary, 5 Associated.
- 33 LINK instances represent 27 clinical relationships in the reference specification. Two SOAP notes each represent one clinical unit but comprise four technical `OBSERVATION.progress_note.v1` ENTRYs, so each SOAP episode assignment expands to four LINKs.
- EP1 (“General Health Problem”) is a default episode, not a parent episode.

## Verification summary

| Verification | Result |
|---|---|
| REST persistence of CE and EP LINKs | PASS |
| AQL retrieval of 9 encounter LINKs | PASS |
| AQL retrieval of 24 episode LINKs | PASS |
| Consolidated EP query (24 rows) | PASS (2026-10-19 06:59:06.997654752 UTC) |
| Exactly one Primary relationship for each of the 19 referenced ENTRYs | PASS, verified from returned LINK dataset |
| Five additional Associated relationships without clinical content duplication | PASS |
| SOAP note: four technical ENTRYs share the same Primary episode | PASS in dataset |
| Selective MR1 Blood Pressure retrieval through a separate AQL query | PASS |
| Native `DV_EHR_URI` LINK-target dereferencing | Not demonstrated |
| Server-side enforcement of clinical relationship invariants | Not demonstrated |
| Version-update propagation / dangling reference handling | Not tested |
| EP2 relationship resolution (12 Primary LINKs, six MR COMPOSITIONs) | PASS (T2.7a) |
| EP2 clinical ENTRY retrieval (12 ENTRYs across six MR COMPOSITIONs) | PASS (T2.7b) |
| Chronological EP2 clinical view assembly | PASS (manual assembly from retrieved results, T2.7c) |
| Automated end-to-end LINK traversal and view assembly | Not implemented or tested |

## Interpretation

The PoC demonstrates that standard openEHR LINKs can persist and expose episode-to-ENTRY and encounter-to-COMPOSITION relationships in the tested EHRbase environment. It does not establish automatic dereferencing of LINK targets. Application-side interpretation and additional AQL queries were required to selectively retrieve clinical ENTRY content in the demonstrated test.

See [`T2-link-implementation.md`](T2-link-implementation.md) for the technical design and [`T2-link-test-identifiers.md`](T2-link-test-identifiers.md) for the canonical identifiers and documented verification evidence. The EP2 clinical view was assembled manually from 12 separately retrieved ENTRYs. Automated LINK traversal and assembly were not implemented.

AQL evidence: The executed AQL queries and observed results are documented in [`T2-link-test-identifiers.md`](T2-link-test-identifiers.md). Complete AQL response payloads were not separately archived.
