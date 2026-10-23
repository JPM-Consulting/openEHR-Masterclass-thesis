# T2 — Evidence Manifest (LINK Pattern)

Scope: Archived artifact inventory for the T2 LINK-based proof of concept. Source: `reproducibility(3).zip`, `08-technical-proof-of-concept/04-link-pattern/T2/`. Integrity method: SHA-256 calculated from the original archived file bytes.

## Evidence summary

| Category | Files |
|---|---:|
| `json/requests/` | 10 |
| `json/persisted/` | 15 |
| `documentation` | 3 |

Total: 28 files, excluding ZIP directory entries and macOS metadata.

## Test evidence and interpretation

- The ten request JSON files include exploratory and unsuccessful test variants. They must not all be interpreted as successful final persistence operations.
- The 15 `json/persisted/` files are archived final COMPOSITION exports (MR1–MR9, CE1–CE2, and EP1–EP4), described as GET exports in the [T2 README](README.md).
- [T2 test identifiers](T2-link-test-identifiers.md) documents executed AQL queries and observed outcomes, including EP2 reconstruction. Complete AQL response payloads were not separately archived.
- The stored LINK relationships comprise nine encounter LINKs and 24 episode LINKs (19 Primary and five Associated), according to the T2 documentation. This manifest inventories files and hashes. It does not independently verify test execution.
- The archive contains version-specific identifiers. Replay in another EHR requires identifier remapping and the correct operation order.

## Archived files and SHA-256

The checksums below describe the files in the source archive. Editorial revisions to the three Markdown documents listed here will change their SHA-256 values. Recalculate those entries after integrating the revised documents. Checksums verify file identity against the recorded values, not historical provenance.

| Relative path | SHA-256 |
|---|---|
| `README.md` | `dd3e1139d4a4d63eed5319d06f158cbc7f2100e044d18d62821b86a7482d81da` |
| `T2-link-implementation.md` | `8678cfad072401db44024c2eac0fb10cae405220015e7960d2aa472339e84fbc` |
| `T2-link-test-identifiers.md` | `767cbe2a3a652167749167bd49611c9a96a6bccd4c066d967b91cb91f2a34aad` |
| `json/requests/T2.2c-CE1-link-MR1-smoke-test.json` | `3d88a5f3007c0f0a6bf2d161194a2e1cdad2744df605750d8bb82abf01616d35` |
| `json/requests/T2.3a-CE1-PUT-links-MR1-MR5.json` | `18445bce3f64b49094565adbc628ab17de74c87a4368ce5cbd5545e0aae744fa` |
| `json/requests/T2.3c-CE2-POST-links-MR6-MR9.json` | `030b2386946e54a9c1aff22a2b046025600c7f2bdf294171f91da1b38d123525` |
| `json/requests/T2.4b-EP1-CR-010-smoke-test-URI-encoded.json` | `bafb2dc831e611a9c3c57ddf6b3c9f2c77824e159afa2dc81ebdb5c3cd367aa0` |
| `json/requests/T2.4b-EP1-CR-010-smoke-test.json` | `d3af2516e27721011976ac54c5027e6e73e12f4b833df50455788815e2f7c441` |
| `json/requests/T2.4e-EP3-CR-011-associated-smoke-test.json` | `fb9ab64fa554ab0f44a0e7a3f0d703777e84b02c45e7d55f7a05446c404c1015` |
| `json/requests/T2.5b-EP1-PUT-7-primary-links.json` | `5e6a565bf288ac57c62857598c9aeb0e9c1209d93a177788dc69a843a594c3f4` |
| `json/requests/T2.5b-EP2-POST-12-primary-links.json` | `75904f7ec200144a621163322689e5f6cafa5aa6f06e1ad37bf5d784425611e4` |
| `json/requests/T2.5b-EP3-PUT-2-associated-links.json` | `5496943abbcca08caac8a0f077ea9f5971066eabf3327eed9a7f0a59443911b0` |
| `json/requests/T2.5b-EP4-POST-3-associated-links.json` | `751e8cae16ac842a3cacf604b594023a322c0db9187d29ec9839a00cf0c4c6a4` |
| `json/persisted/T2-CE1-final.json` | `a6c270dca305d9fcb6877d8f3e3f98b5ba51f1ec895a3a3dcea0ec285daefe96` |
| `json/persisted/T2-CE2-final.json` | `151ed9e5d6436b29cdb366274010aaa867d4390193dd9d16d52b57bb7a6519d1` |
| `json/persisted/T2-EP1-final.json` | `2347c0493549d9e1c44787d827379586c78b974a4bd95ae84fdbe4f194c287bd` |
| `json/persisted/T2-EP2-final.json` | `e90e866af0bb32d6219063302615c1092db8b8e57b1d317028d03c1184ac9749` |
| `json/persisted/T2-EP3-final.json` | `8b216a1564c9c5e2f25105bc8d9481842974073db5dd6c0c8a08bfd6f5f16ece` |
| `json/persisted/T2-EP4-final.json` | `8b78820323c3c8b49173a43e813693d609acc54116b555da57b98fb1e3b205ab` |
| `json/persisted/T2-MR1-final.json` | `3dfd06539c3a95807f5fb805debd67a399b6f912651b8ba7d925fe56d6f6491d` |
| `json/persisted/T2-MR2-final.json` | `6889732bb3355e615d7ae2720c5cad7a187d21a226b4e5a84e8d457d98ee426e` |
| `json/persisted/T2-MR3-final.json` | `ce566a406feb0d483cdd0191f80645520545251f2eee53060529bad9ed7b3fd7` |
| `json/persisted/T2-MR4-final.json` | `f30ee0e92200381878ad01e18123853aa5923a6aac8166e10a55033baa8f38dc` |
| `json/persisted/T2-MR5-final.json` | `05bb7b171035bd71fc8307b7730d939da91b6ec858f6b8cfbd6c46229306085b` |
| `json/persisted/T2-MR6-final.json` | `aae464d96be6a5485cdebf4d3e7e6c75f55cc2bcd7d04bb3fa882da06e5496fb` |
| `json/persisted/T2-MR7-final.json` | `2dc20c2d81833e9e2f1d3f923a8d1bea834e03721536dc901d0992236996dd91` |
| `json/persisted/T2-MR8-final.json` | `d6168cfdc56908d91dcdebbdc90b437b5e31c954a371765f166afed66bb440e1` |
| `json/persisted/T2-MR9-final.json` | `669bc8d87ba1f44eb59016cb5d7add0352f31e9dbadd00873932e84860406dcf` |

## Persisted COMPOSITION identifiers

| Export | Versioned COMPOSITION UID |
|---|---|
| `json/persisted/T2-CE1-final.json` | `677552a4-fd78-4678-b91c-0172bc118017::local.ehrbase.org::2` |
| `json/persisted/T2-CE2-final.json` | `4805a3a9-7518-4bd8-9f5f-e57bcfcb30c2::local.ehrbase.org::1` |
| `json/persisted/T2-EP1-final.json` | `6e963022-99a0-45ff-803b-24b835f254ce::local.ehrbase.org::2` |
| `json/persisted/T2-EP2-final.json` | `9f04a0d0-1eed-4688-9d19-04cf3f1d5210::local.ehrbase.org::1` |
| `json/persisted/T2-EP3-final.json` | `e7aaa7a9-c8d9-4533-8725-9c51d4d7e003::local.ehrbase.org::2` |
| `json/persisted/T2-EP4-final.json` | `81bcb7b2-7db7-480c-abcd-9c5441e51f73::local.ehrbase.org::1` |
| `json/persisted/T2-MR1-final.json` | `5f73b7ab-3b72-4951-9c75-a8336c37b5ac::local.ehrbase.org::1` |
| `json/persisted/T2-MR2-final.json` | `7e606fc5-6a49-4c97-ab52-4167f045c6d7::local.ehrbase.org::1` |
| `json/persisted/T2-MR3-final.json` | `3c02c656-c63d-4944-b06d-c32c7e2ddcf8::local.ehrbase.org::1` |
| `json/persisted/T2-MR4-final.json` | `cbe82162-bacc-41a5-a252-575fb5bafbbd::local.ehrbase.org::1` |
| `json/persisted/T2-MR5-final.json` | `c1c90004-961b-4a09-9ed3-c67cde8027fb::local.ehrbase.org::1` |
| `json/persisted/T2-MR6-final.json` | `bd64397e-9a0b-4fc1-af59-720c3d7f0eaa::local.ehrbase.org::1` |
| `json/persisted/T2-MR7-final.json` | `22b21098-90d0-4c56-9ba1-0244436a6ee0::local.ehrbase.org::1` |
| `json/persisted/T2-MR8-final.json` | `1a226cc5-7f59-45f9-9833-42d976d3c63c::local.ehrbase.org::1` |
| `json/persisted/T2-MR9-final.json` | `71c9f21b-9165-4fb4-9fa2-343486fcf37a::local.ehrbase.org::1` |

## Limitations

This inventory does not establish native LINK target dereferencing, automatic clinical-view assembly, or repository-enforced referential integrity. Refer to the [T2 README](README.md), [T2 implementation](T2-link-implementation.md), and [T2 test identifiers](T2-link-test-identifiers.md) for the documented test scope, observed results, and limitations.
