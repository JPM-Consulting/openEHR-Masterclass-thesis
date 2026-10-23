# T3 — Evidence and Provenance Manifest

## Archive Inventory

The archived T3 evidence includes nine canonical JSON request bodies (MR1–MR9) in [`json/requests/`](json/requests/) and 15 final persisted COMPOSITION JSON exports (CE1–CE2, EP1–EP4, MR1–MR9) in [`json/persisted/`](json/persisted/). The persisted exports contain server-assigned versioned `COMPOSITION.uid` values.

This inventory supersedes an earlier description reporting seven requests and missing GET exports. JSON parsing and comparison with the SHA-256 values below verify the integrity of the files in the reviewed archive relative to this manifest. They do not independently establish historical provenance or reproduce REST GET requests against the live server. The documented interactive test session separately records successful REST GET requests for MR1–MR9.

## Request Bodies (9)

| File | SHA-256 |
| --- | --- |
| `T3-MR1-vital-signs-with-links.json` | `1cad813c57b5ecf33dca47601c61f4afb5c834aa0a7f5f09c76de24df12cc2d4` |
| `T3-MR2-body-measurements-with-links.json` | `462041498b988229a599753e6cbf5e3351ff5a25ef618a93a6bf35bc4c033b9d` |
| `T3-MR3-urinalysis-with-links.json` | `1713a924c5c043e6c8dcc281c496ebf39807783e587c14b2d08b34e305348a9c` |
| `T3-MR4-soap-progress-note-with-links.json` | `b9f1c75946682e4ab1c5e716cd25f4946af52168f4997fffa81cc2f0d5206532` |
| `T3-MR5-medication-order-with-links.json` | `9d0b987b78e758e593d4df720f6d3601933d8a196f9c64c6bcbbe64d4836999f` |
| `T3-MR6-microbiology-result-with-links.json` | `4ab4f8953d20150da4999ef9a2155daa10177d9bceac93afe31b8576e3e3fd69` |
| `T3-MR7-vital-signs-with-links.json` | `e10e199a9541f15736a062d6e74a1ed1c5385ed58cb31b723bb674e24785402f` |
| `T3-MR8-soap-progress-note-with-links.json` | `123436093428e3e302928b4c05b98acf56255c6fa16523936ea96abb1b75b7b0` |
| `T3-MR9-medication-order-with-links.json` | `c7bb81cc04d4c6a0c0404ca64d5ad595c59125e91c6429e46affcba431737212` |

## Persisted COMPOSITION Exports (15)

| File | Versioned COMPOSITION UID | SHA-256 |
| --- | --- | --- |
| `T3-CE1-final.json` | `a942e76a-471d-4e43-9d8b-e9318c2c0498::local.ehrbase.org::1` | `79af5be3137b48baec2ead6785378b5392ca509c706a55ed3cc4ee5ca43cb7ea` |
| `T3-CE2-final.json` | `4612e7a1-047a-466c-a5bf-42be2711f044::local.ehrbase.org::1` | `94f0fca947b7a55c004cab479d5002d83982467c8f1fb753579ec78d7f63b574` |
| `T3-EP1-final.json` | `25e56fbc-9c74-4c6e-8ce9-a3e97a0250b1::local.ehrbase.org::1` | `e09bccbcf2c876c158a1339aeb0b4e9963112441cdb75855a2f7bbd19c7164eb` |
| `T3-EP2-final.json` | `12ac2566-fec2-46c2-a28b-fcc7ac40d6f8::local.ehrbase.org::1` | `739c5d0888094e3a6fd63a0f6dda909d412828e5ede73f0687dea278b05dd466` |
| `T3-EP3-final.json` | `4e2fa228-1857-4a60-9cc1-53a6d7f54a00::local.ehrbase.org::1` | `f50ca046b082f1c336de9b4be17557a996c33385035cc7a7954d5748d5f0b5d9` |
| `T3-EP4-final.json` | `50a0b2b8-9a3c-46f5-b802-0b634f75415b::local.ehrbase.org::1` | `11a6aaef4edb6f5fe3c89c5dc158337a29c78f1c750803ff44a50072638c5d34` |
| `T3-MR1-final.json` | `74b167c9-faa7-4716-b653-c0644b85b9f5::local.ehrbase.org::1` | `5d83a69ce9a728448bcb3dd24938ac6409cd8a4c04c3da1c5f315402bb237f61` |
| `T3-MR2-final.json` | `c93029ec-3295-4a70-bd4d-37d5d010d029::local.ehrbase.org::1` | `7cd9667a7863b57038648d65e9d6ae50073d4134b4c5e8419ed45396dbbbbb48` |
| `T3-MR3-final.json` | `75462d29-d528-4991-8543-42ee971cab25::local.ehrbase.org::1` | `479cc94eb733f18ba2e91e6b009d3a7993acc93a0833b3211efd9b485bcb68b0` |
| `T3-MR4-final.json` | `7f2afe1e-9c14-4f36-88e1-e3edb5d50c4f::local.ehrbase.org::1` | `e00eecf0f535a5ae000c515dd44f7bfbf2169ea14f6ccccd913aeda0f82b98cc` |
| `T3-MR5-final.json` | `8817d768-f57a-48ae-a1a3-768f89db6ed9::local.ehrbase.org::1` | `cc9ea31baa445526b1384a67f549a71bf441c708ea34c33ae1be5117bb4b2c71` |
| `T3-MR6-final.json` | `1f0eaddc-8750-4fe0-a4a8-3162fa2383a3::local.ehrbase.org::1` | `856127dffa6d4b8177a1d857ed0c69f87e1085628f1648c89d3923e89fca5d5a` |
| `T3-MR7-final.json` | `475ea309-9de7-4033-9589-24fa6a84aa7a::local.ehrbase.org::1` | `9e1ed2097d4d007494e3f85bbd83314bf292aa348679049dcaab8b1cf0aa376c` |
| `T3-MR8-final.json` | `f0116bb9-2067-431f-b3c2-6c0fab9d9e09::local.ehrbase.org::1` | `815a2db59e8647acbe9028ac47d9c3a5cae22ba091e217de28153ecdc4c2c573` |
| `T3-MR9-final.json` | `0f7b9524-7308-4321-8e6f-6cd23aad9d22::local.ehrbase.org::1` | `d24765b0a017a3a0fcaf42ac048db0f0e1c73ecb977fcd9c960fe2674fb0f6f0` |

## Evidence Boundaries

- `json/requests/` contains archived request payloads. Their presence alone does not establish successful submission. `json/persisted/` contains exports of the documented stored state.
- The nine persisted MR exports contain encounter and episode relationship LINKs. The six CE/EP context exports represent the referenced targets and do not contain reverse LINKs in T3.
- The JSON exports do not demonstrate native `DV_EHR_URI` dereferencing, automatic clinical-view assembly, or server-enforced Primary uniqueness. None of these capabilities is claimed as verified.
- Clinical tests and AQL query results are documented in [`T3-link-test-results.md`](T3-link-test-results.md) and [`T3-aql-query-catalog.md`](T3-aql-query-catalog.md). Separate AQL response files and Postman collection exports are not included in the reviewed archive.
