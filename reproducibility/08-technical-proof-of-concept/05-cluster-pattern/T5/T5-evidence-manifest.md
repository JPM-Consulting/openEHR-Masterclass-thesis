# T5: Evidence Manifest

## Archived POST Request Payloads

The SHA-256 values in this manifest identify the archived files in this repository snapshot. They can be checked against the corresponding file bytes and do not, by themselves, establish byte-for-byte equivalence with the original execution artifacts.

| File | SHA-256 | Template |
|---|---|---|
| `json/requests/T5-MR1-post-request.json` | `7b53f86ce45cb26a7e004ed1ebd8f1cc8d8ee3d670d80b525c3fdbc41b3ff65f` | `JPM_Medical_Record_Vital_Signs_Cluster.v1` |
| `json/requests/T5-MR2-post-request.json` | `106762ddf40bfdd2e5aa3896ab1b69b5b339b94a54863f441769532c33e3e688` | `JPM_Medical_Record_Body_Measurements_Cluster.v1` |
| `json/requests/T5-MR3-post-request.json` | `2c3957eb78801af58a53d4401a8b0d1938db436761533436c0ddfc659788abfe` | `JPM_Medical_Record_Urin_Analysis_Cluster.v1` |
| `json/requests/T5-MR4-post-request.json` | `eeb22e9d7d3b3a45453ef67ca31524ae3dedd01a0018b8bce0726f20571ed88d` | `JPM_SOAP_Progress_Note_Cluster.v1` |
| `json/requests/T5-MR5-post-request.json` | `335bdc2c47dae20f5b85590340dc95ffc335e788b58fd629fa42dba70e07457c` | `JPM_Medical_Record_Medication_Order_Cluster.v1` |
| `json/requests/T5-MR6-post-request.json` | `a044e60f963710c51399ecdc0a083823aa44759c02e0f5bc39d066483d2f667a` | `JPM_Medical_Record_Microbiology_Result_Cluster.v1` |
| `json/requests/T5-MR7-post-request.json` | `0f6e0635ff27d9b1f5317220fca5f85b2cf12ace5be31db2aa57f636ad87eb39` | `JPM_Medical_Record_Vital_Signs_Cluster.v1` |
| `json/requests/T5-MR8-post-request.json` | `9bc15a965411f2f45bd3730e72a810de37738f708612021360f2d4981895fc66` | `JPM_SOAP_Progress_Note_Cluster.v1` |
| `json/requests/T5-MR9-post-request.json` | `eddd586a7489fb279c401926bf60c8eec32693ad2789e57d8aba74f2df075da4` | `JPM_Medical_Record_Medication_Order_Cluster.v1` |
| `json/requests/T5-RI-02-invalid-episode-reference.json` | `a15f90e09b542e5729df5afd78237db3ed561e4a8d24593eb69d53d0dd4f265b` | `JPM_Medical_Record_Medication_Order_Cluster.v1` |

## Evidence Coverage and Provenance

- **Archived request payloads:** The nine MR1–MR9 POST request JSON files and the additional RI-02 negative-test request are included in `json/requests/`. AQL request bodies were reconstructed from the recorded test session.
- **Persisted exports:** Sixteen JSON files are archived in `json/persisted/`, representing 15 regular COMPOSITIONs and one additional RI-02 negative-test COMPOSITION. According to the researcher's account, these files were retrieved from the openEHR CDR through REST GET requests at the end of the T5 execution.
- **Evidence not archived:** Raw POST response payloads and complete AQL response payloads were not separately preserved. The observed HTTP statuses and AQL result counts are reported in [T5 test results](T5-cluster-test-results.md).
- **Provenance limitation:** The archived bytes and their SHA-256 checksums can be verified against this repository snapshot. The original REST GET operations were not independently repeated, and historical byte-for-byte equivalence with the original execution artifacts has not been independently established.
- **Artifact distinction:** The POST request bodies in `json/requests/` are not interchangeable with the server-retrieved COMPOSITION exports in `json/persisted/`.

### Archived REST GET COMPOSITION Exports

| File | SHA-256 |
|---|---|
| `json/persisted/T5-CE1-final.json` | `208a49b3fe74679fe855f2707f8333aaacf87238c96aefa5cf2b35b86d522fcb` |
| `json/persisted/T5-CE2-final.json` | `2bc9663194e65ce05e5c3ef6e5a36650631d7347c38a9300ab2355d305cb5002` |
| `json/persisted/T5-EP1-final.json` | `1d2ac8a5d3b5ade2f23e78ae31c854e273526891ffee9fc663b3b29992db2dc3` |
| `json/persisted/T5-EP2-final.json` | `5f5207c0fac00f0a95c8c91b958d5e721c8d936c0c434a573475509f7229737b` |
| `json/persisted/T5-EP3-final.json` | `9cc46cdb96c744f8e28d20605aa42933c2d0db62566204296a6434e062f9705c` |
| `json/persisted/T5-EP4-final.json` | `ffb1951177045250d4c8af1150b7cc253dd2421c7db5ec6e2622d457b3383ef0` |
| `json/persisted/T5-MR1-final.json` | `789bc7149179d68bf1831ad8d09ecc1c0e07709853cca68b4e3348fe9a12196c` |
| `json/persisted/T5-MR2-final.json` | `c7335199487bc9e6091e61a8fcb35888528e2b2ce26958c99dba4b1ad34940f5` |
| `json/persisted/T5-MR3-final.json` | `be672645a198f6378b850ec30b64d89b3a93d06db45a9f25eef9a27039291928` |
| `json/persisted/T5-MR4-final.json` | `da702eaf572b035d61441a1db813a09cf09254be1f7bb548b154578690b051c1` |
| `json/persisted/T5-MR5-final.json` | `292385214d2e370c4b3015f08faab9d5915c9c0fea20c17f166d79b1fa4fe521` |
| `json/persisted/T5-MR6-final.json` | `3e28d2c3979539085364d3f8f3ce52036ffbece07d6c07cb8ed68e1dcc7bd92b` |
| `json/persisted/T5-MR7-final.json` | `bf6caa8e6b3b98566a15ee725d83a610f4b7311056ebd9dd4d62f40c2e0927c9` |
| `json/persisted/T5-MR8-final.json` | `20c8a6c3a4c719e54661a3809758630eba86d9eedd794758333d5daa51e63e0b` |
| `json/persisted/T5-MR9-final.json` | `b695d1b7b265e6fd3beaf7f2ec31d1297bb3b7a3d23b018dc5cb390ce9c408f2` |
| `json/persisted/T5-RI-02-persisted.json` | `4e3d14b0ea69a64e466315248678b6d5a9406fa185aeeb0658115e5f2b09783f` |

## Reproduction Notes

- EHR: `16fe2926-c82a-462c-93f2-d5e67a29656f`. System: `local.ehrbase.org`. Versioned identifiers are documented in [T5 test identifiers](T5-cluster-test-identifiers.md).
- The RI-02 COMPOSITION is an additional negative-test artifact and must be excluded when reproducing counts for the original 15-COMPOSITION dataset.
- Encode square brackets in AQL paths when they occur in REST URLs. Submitting AQL through POST `/query/aql` avoids these URL encoding issues.
