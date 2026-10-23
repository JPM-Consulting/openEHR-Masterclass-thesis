# T3 — Execution and Verification Log

Scenario: T3 (LINK pattern, Care Encounters and Episodes of Care created first). EHR: `f4908498-afef-4e3c-8cc4-bbdf16d808bf`. Environment: EHRbase 2.30.1, openEHR REST API, canonical JSON, AQL and Postman. Overall result: PASS within the documented test scope.

## Summary by phase

| Phase | Activity | Observed evidence | Status |
|---|---|---|---|
| T3.1 | Create isolated EHR | Isolated EHR ID recorded and used throughout | PASS |
| T3.2 | Persist CE1 and CE2 | Both context COMPOSITIONs persisted, version `::1` | PASS |
| T3.3 | Persist EP1–EP4 | Four context COMPOSITIONs persisted, version `::1` | PASS |
| T3.4 | Persist nine MR COMPOSITIONs with LINKs | MR1–MR9 POST HTTP 201, independent GET HTTP 200, and all 33/33 LINK instances persisted | PASS |
| T3.5 | Query stored relationships | Inventory 15, encounter LINKs 9, OBSERVATION LINK rows 22, INSTRUCTION LINK rows 2 | PASS |
| T3.6 | Reconstruct clinical content and verify integrity | EP2 12 technical ENTRYs in six documents, clinical details retrievable, with all nine MR JSON structures individually inspected | PASS within tested scope |
| T3.7 | Validate longitudinal and associated episode views | EP2 6/6 MR documents, EP3 2/2 BP observations, and EP4 3/3 body measurements. Evaluation reused earlier AQL tests without additional HTTP calls | PASS within tested scope |

## T3.5 — AQL relationship retrieval

| Test | Observation | Status |
|---|---|---|
| T3.5.1 | Inventory: 15 COMPOSITIONs = 2 CE + 4 EP + 9 MR | PASS |
| T3.5.2 | Nine encounter LINKs on MR COMPOSITIONs, plus six context COMPOSITIONs without encounter LINK | PASS |
| T3.5.3 | MR1 OBSERVATION LINKs: three rows (BP primary EP1, BP associated EP3, pulse primary EP1) | PASS |
| T3.5.4 | 22 OBSERVATION LINK rows: 17 primary and 5 associated. MR1 3, MR2 6, MR3 1, MR4 4, MR6 1, MR7 3, MR8 4 | PASS |
| T3.5.5 | Two INSTRUCTION LINK rows: MR5 and MR9 primary EP2 | PASS |

AQL row semantics: The same clinical ENTRY may produce multiple rows when its `links` array has multiple items. This does not mean clinical ENTRYs are duplicated. Primary uniqueness was confirmed by inspecting the persisted JSON, not by the aggregate count alone.

## T3.6 — Detailed evidence

| Test | Observed result | Status |
|---|---|---|
| T3.6.1 | Inverse EP2 OBSERVATION link filter: 10 ENTRY-level rows | PASS |
| T3.6.2 | Inverse EP2 INSTRUCTION link filter: 2 medication orders | PASS |
| T3.6.3 | SOAP SECTION traversal returned 16 rows instead of 8 because parent `SOAP headings` and four leaf sections both matched | PARTIALLY VERIFIED, refined in T3.6.4 |
| T3.6.4 | Excluding `SOAP headings` returned 8 leaf-section rows (4 per SOAP document) | PASS |
| T3.6.5 | MR3 urinalysis JSON/AQL: leukocytes 3+, nitrite Positive, blood 1+, protein Trace, pH 6.0 | PASS |
| T3.6.6 | Targeted leukocytes node `[at0068]`: ordinal 5, clinical symbol `3+` | PASS |
| T3.6.7 | All five urinalysis symbols returned in one AQL row | PASS |
| T3.6.8 | MR6 nested microbiology result: *E. coli*, five susceptibility tests | PASS |
| T3.6.9 | Direct OBSERVATION→`CLUSTER[at0009]` failed (HTTP 400 without OBS archetype predicate), corrected query returned 0 due to missing intermediate microbiology CLUSTER | FAIL for attempted query, corrected in T3.6.10–11 |
| T3.6.10 | Explicit `CLUSTER.lab_microscopy_culture.v0` retrieved nested microbiology content | PASS |
| T3.6.11 | Nested `CONTAINS CLUSTER susceptibility[at0009]` returned five correct agent/interpretation pairs | PASS |
| T3.6.12 | `SELECT DISTINCT` inverse EP2 query returned six MR COMPOSITIONs across two dates | PASS |
| T3.6.13 | Added MR COMPOSITION encounter LINK target: six MR documents assigned to CE1/CE2 | PASS |
| T3.6.14 | `GROUP BY` syntax rejected with HTTP 400. This syntax is not part of standard AQL, application-side aggregation required | N/A — unsupported syntax |
| T3.6.15 | EP2 filtered to CE1: MR3, MR4, MR5 (3 documents) | PASS |
| T3.6.16 | EP2 filtered to CE2: MR6, MR8, MR9 (3 documents) | PASS |
| T3.6.17 | Associated EP3 filter: MR1 and MR7 BP (2) | PASS |
| T3.6.18 | All BP links: four rows (2 observations × primary/associated) | PASS |
| T3.6.19 | Associated EP4 filter: MR2 height, weight and BMI (3) | PASS |
| T3.6.20 | Primary EP1 filter: seven OBSERVATION links | PASS |
| T3.6.21 | Polymorphic `CONTAINS ENTRY`: 19 primary links, but count alone does not prove one per ENTRY | PASS for count |
| T3.6.22 | MR4 SOAP: four progress-note observations with the same archetype/name, all linked as primary EP2 | PASS |
| T3.6.23 | MR4 SOAP `entry/uid/value` returned four nulls | PASS (optional UID absent) |
| T3.6.24 | MR4 persisted JSON: four child sections S/O/A/P, exactly one primary EP2 link per observation, and one CE1 encounter link | PASS |
| T3.6.25 | MR8 persisted JSON: four child sections S/O/A/P, exactly one primary EP2 link per observation, and one CE2 encounter link | PASS |
| T3.6.26 | MR1 GET: BP primary EP1 + associated EP3, pulse primary EP1, COMPOSITION→CE1 | PASS |
| T3.6.27 | MR2 GET: height, weight, BMI each primary EP1 + associated EP4, COMPOSITION→CE1 | PASS |
| T3.6.28 | MR7 GET: BP primary EP1 + associated EP3, pulse primary EP1, COMPOSITION→CE2 | PASS |
| T3.6.29 | MR3 GET: urinalysis primary EP2, COMPOSITION→CE1 | PASS |
| T3.6.30 | MR5 GET: medication INSTRUCTION primary EP2, COMPOSITION→CE1 | PASS |
| T3.6.31 | MR6 GET: microbiology OBSERVATION primary EP2, COMPOSITION→CE2 | PASS |
| T3.6.32 | MR9 GET: medication INSTRUCTION primary EP2, COMPOSITION→CE2 | PASS |

## Clinical reconstruction of EP2

CE1 (2024-11-15): MR3 urinalysis (leukocytes 3+, nitrite positive), MR4 SOAP (dysuria, pyuria, suspected cystitis, antibiogram requested), MR5 empirical trimethoprim–sulfamethoxazole (TMP 160 / SMX 800 mg, oral 2×1, 12-hour interval).

CE2 (2024-11-17): MR6 urine culture *Escherichia coli*, resistant to TMP–SMX and ciprofloxacin, sensitive to amoxicillin–clavulanate, nitrofurantoin and fosfomycin. MR8 SOAP documents persistent symptoms and treatment switch. MR9 amoxicillin 500 mg/clavulanate 125 mg, oral 3×1, 8-hour interval.

SOAP clinical integrity: Each SOAP note remains one clinical unit, its four technical OBSERVATIONs all carry the same primary EP2 LINK. Two SOAP COMPOSITIONs account for eight of the 12 EP2 technical ENTRYs.

## T3.7 — Final view validation (reuse of existing evidence)

- T3.7.1 PASS: Six distinct EP2 clinical MR COMPOSITIONs, three CE1 and three CE2, identified using `SELECT DISTINCT` and MR encounter links (T3.6.12–16).
- T3.7.2 PASS: EP3 two associated BP observations (MR1, MR7), EP4 three associated body measurements (MR2) (T3.6.17–20).
- T3.7.3 PASS within tested scope: Inverse LINK lookup and application-level reconstruction demonstrated for the documented views without duplicating clinical content, automatic view generation and native dereferencing not tested.

## Exceptions and limitations

- AQL `SECTION s CONTAINS OBSERVATION o` includes ancestor and descendant sections. parent/leaf filtering needed to avoid double counting.
- `GROUP BY` is not part of standard AQL. the failed test T3.6.14 is N/A, not an EHRbase defect.
- AQL at-code `CONTAINS` traversal requires an appropriate archetype predicate and the correct intermediate CLUSTER level. see T3.6.9–11.
- Clinical `DV_ORDINAL` labels are read via `symbol/value`. raw numeric ordinal values are not the clinical display strings.
- The `DV_EHR_URI` LINK target is stored and searchable, but automatic dereferencing was not demonstrated.
- No repository-enforced primary-link cardinality, automatic reference-integrity checks, performance, concurrency, historical version resolution, or full eight-user-story/six-criterion evaluation demonstrated.
- Original Postman raw response exports for every AQL call were not supplied as separate files, the observations above are documented from the sequential test session. Available request JSONs are catalogued separately.

## Conclusion

T3 PASS within the documented test scope: 15 COMPOSITIONs, 19 technical ENTRYs, 33 persisted and retrievable LINKs, EP2 12 technical ENTRYs / 6 documents / 2 encounters, EP3 2 and EP4 3 associated observations. T3 demonstrates context-first creation and inverse retrieval supporting the documented episode-oriented views. Native LINK dereferencing and automated view generation were not demonstrated.
