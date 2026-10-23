# T5 — Executed Tests and Outcomes

## Execution Evidence

The results below were recorded during the interactive Postman test session on 21 October 2026. The evidence consists of documented HTTP status codes, AQL result counts, and selected response payloads. Complete response payloads were not archived as files in this package. The accompanying AQL files contain reconstructed requests rather than response exports. The results have not been independently re-executed for this editorial review.

## Persistence

| Test | Action | Outcome |
|---|---|---|
| T5.1 | Create EHR | PASS (201) |
| T5.2 | POST and independent GET for CE1–CE2 | PASS (201/200) |
| T5.3 | POST and independent GET for EP1–EP4 | PASS (201/200) |
| T5.4 | POST and independent GET for MR1–MR9 | PASS (201/200) |
| T5.5 | AQL-01–AQL-12 and independent GET for EP2 | PASS within the tested scope |
| T5.6 | RI-01–RI-04 | Negative-test execution completed. Referential integrity was not enforced in the tested case. |

## AQL Evidence

| Test | Focus | Result size | Finding |
|---|---|---:|---|
| AQL-01 | Original COMPOSITION inventory (before RI-02) | 15 | 2 CE + 4 EP + 9 MR |
| AQL-02 | ENTRY relationship CLUSTER | 19 | All clinical ENTRYs located |
| AQL-03 | URI and episode role | 24 | 19 Primary, 5 Associated |
| AQL-04 | EP2 longitudinal ENTRY view | 12 | MR3/4/5/6/8/9 |
| AQL-05 | CE2 contact view | 8 | MR6/7/8/9 |
| AQL-06 | CE2 and EP2 intersection | 6 | MR6/8/9 |
| AQL-07 | Associated role code `at0155` | 5 | EP3 ×2, EP4 ×3 |
| AQL-08 | EP3 blood pressure clinical data | 2 | 140/90 and 142/85 mm[Hg] |
| AQL-09 | MR8 SOAP content and references | 4 | Same CE2 and EP2 Primary across all four ENTRYs |
| AQL-10 | Nested SOAP SECTIONs | 8 | Four parent and four child SECTION matches, not eight ENTRYs |
| AQL-11 | SOAP child SECTION filter | 4 | S/O/A/P texts extracted without duplicates |
| AQL-12 | Longitudinal EP2 SOAP | 8 | MR4 and MR8, each with four parts assigned to EP2 Primary |

The AQL-12 evidence records two SOAP notes. MR4 (15 November): Subjective, burning urination for three days. Objective, pyuria. Assessment, suspected cystitis. Plan, antibiogram and empirical TMP–SMX. MR8 (17 November): Subjective, persistent symptoms. Objective, *E. coli* resistant to the current antibiotic. Assessment, acute bacterial cystitis. Plan, change antimicrobial therapy. AQL-12 orders by COMPOSITION context time but does not guarantee the S/O/A/P sequence when timestamps are identical. SECTION identity is needed to distinguish the SOAP components. Each four-ENTRY SOAP note remains one clinical documentation unit.

## Independent Target GET

An independent GET for EP2 (`c2ad3baa-50c4-4b00-8177-4d86352b7e89::local.ehrbase.org::1`) returned HTTP 200. The documented response identified `JPM_Episode_of_Care_Cluster.v1`, `openEHR-EHR-COMPOSITION.problem_list.v2`, and the diagnosis Urinary tract infection with Active, Acute, and Current qualifiers. This demonstrates retrieval of a known target by an explicit GET request, not automatic URI dereferencing.

## Referential-Integrity Negative Tests

| Test | Result | Evidence |
|---|---|---|
| RI-01 | PASS (precondition) | AQL returned zero matches for the absent UID |
| RI-02 | POST accepted (201) | New UID `056c6620-67b0-408f-bf90-1f8458fe8b66::local.ehrbase.org::1` contains an absent EP URI |
| RI-03 | GET succeeded (200) | Invalid EP URI remained unchanged |
| RI-04 | AQL returned one row | Contact CE1, absent EP URI, Primary |

The absent RI-02 target was `ehr://00000000-0000-4000-8000-000000000099::local.ehrbase.org::1`. The acceptance of this reference demonstrates a referential-integrity limitation in the tested EHRbase environment. It is not evidence of successful integrity enforcement and should not be generalized to other repositories or configurations. Following RI-02, the test EHR contained 16 COMPOSITIONs and 20 ENTRYs, whereas the original dataset contained 15 COMPOSITIONs and 19 ENTRYs. Including RI-02, the documented totals are 35 logical associations and 45 stored URI occurrences.

## Interpretation Limits

- Automatic `DV_EHR_URI` dereferencing was not demonstrated. AQL returned stored URI values and source ENTRY content.
- The RI-02 negative test demonstrated that target existence was not enforced for the tested URI in the documented environment.
- Target resolution was not systematically verified for all 33 original logical relationships.
- Mandatory relationships and consistent episode assignment across an entire SOAP note were not independently tested as server-enforced invariants.
- Query performance, multi-vendor interoperability, and production behavior were not evaluated.
- The recorded test outcomes are supported by the documented interactive execution. Complete response exports are not available for independent replay or verification.
