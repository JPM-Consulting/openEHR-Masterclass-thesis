# T4 Evidence and Provenance Manifest

## Archived Request Payloads

The eight archived JSON request bodies were originally extracted without modification from `requests.zip`. Their SHA-256 values refer to those archived bytes. Request bodies are not independent evidence of successful server execution or GET responses.

| File | DV_EHR_URI values | SHA-256 |
|---|---:|---|
| `T4-CE1-post-v1.json` | 5 | `ed3fd3dff740f8dd874c616c44ad3323365b0a87c719e0ef666d3b06df485f03` |
| `T4-CE2-post-request.json` | 0 | `3be54fab63da47fafee8f82a1b54ba7f06f12529990d1644f2ea89ba7874d5fc` |
| `T4-CE2-put-request.json` | 4 | `a919b32009abbd0b846d027bf80aaa3c76537fe9071a67b082fdc65d330b0e0e` |
| `T4-EP1-post-request-uri-encoded.json` | 7 | `8df1a69547696d7f280b02c0299f38827fcb48a8c310a5dc7b5a9df7db0eb331` |
| `T4-EP1-post-request.json` | 7 | `28c710aeaa76105abbb8c9e7bc58cebcaeb29bfd0ed18994955a6539edb89ec8` |
| `T4-EP2-post-request.json` | 12 | `8129d2f3e7b613e061cd768c1383fe67ea73af90200d276380db6aae1cd379c8` |
| `T4-EP3-post-request.json` | 2 | `85ec3255307218e350ddb8826cd94bc14105636aa5d437e6d5d2e665a9e9f588` |
| `T4-EP4-post-request.json` | 3 | `299d56ff98745458c8c19ea7f0674475485627126c48ffb7e3d344fc987c4aa4` |

The initial EP1 request, `T4-EP1-post-request.json`, failed with HTTP 400 because its URI paths contained unencoded brackets. The corrected `T4-EP1-post-request-uri-encoded.json` succeeded with HTTP 201. These are alternative requests, not two successful EP1 writes. The documented test session records seven successful CE/EP operations: CE1 POST, CE2 POST, CE2 PUT, and EP1–EP4 POST.

## Persisted COMPOSITION Exports (REST GET Response Bodies)

The archive contains 15 final-version COMPOSITION JSON exports originally supplied in `persisted.zip` and a separately supplied historical CE2 version `::1`. SHA-256 values were calculated from the supplied file bytes, not reconstructed content. All 16 files parse as JSON and contain the documented versioned COMPOSITION UIDs. The 15 final-version exports contain 33 stored `DV_EHR_URI` values in total. These offline content checks do not independently establish HTTP status codes, native URI dereferencing, or historical source provenance.

| File | Versioned COMPOSITION UID | DV_EHR_URI values | SHA-256 |
|---|---|---:|---|
| `T4-CE1-final.json` | `125bbcd3-94d7-40d1-95bb-57921bae7134::local.ehrbase.org::1` | 5 | `02322555b5815739a3c05519d46077fb07f1495c4c74bee1c593d5612112eea9` |
| `T4-CE2-final.json` | `ebe7f166-85c0-4c68-bf8a-572f32cc2c3c::local.ehrbase.org::2` | 4 | `cd42c17939d54babf848770f7ad74e75922e2a2072a9e5d5d139304f2403520c` |
| `T4-EP1-final.json` | `63d77635-2e03-48ef-86f5-6614011aea14::local.ehrbase.org::1` | 7 | `b3f87c746f476aff65efc0c139cad33d2f4e1e84569c334945eae8181b75b8df` |
| `T4-EP2-final.json` | `78d056e3-258f-4407-8b65-0130459c194d::local.ehrbase.org::1` | 12 | `77a3988c7cda840698d0ffc3809834a4e35823243635d9c7a9e3f35c807956bb` |
| `T4-EP3-final.json` | `6e827bf6-e492-481c-8da3-129a0e06a690::local.ehrbase.org::1` | 2 | `b840c437bd99391b416a2c1f16ea80f2ea2960b977b312d8806708fc26dcc12d` |
| `T4-EP4-final.json` | `c739a163-b142-430b-adce-7bab517af22d::local.ehrbase.org::1` | 3 | `725034b594bf85aedaf2b2a8bd5a853d2345b178912adb7bff8ec9db2cd0fec0` |
| `T4-MR5-final.json` | `ea5e5931-5d1d-49dc-9ec1-1c6d7adcc676::local.ehrbase.org::1` | 0 | `4ab8e40c00e3a26afc433da768d84329f98fc8df755d2202c30bb58f128afc43` |
| `T4-MR1-final.json` | `1bfd53df-f670-407d-a7bc-bdd6ace292e1::local.ehrbase.org::1` | 0 | `aa975b41294a0ca3a7879d679246a35876bb787cb2fedc123702e548abcf38da` |
| `T4-MR2-final.json` | `6cd82ad3-c4e1-454c-a0f8-b3f75bb3d30c::local.ehrbase.org::1` | 0 | `b5230ebf8f2be9225042549fea6a7958f906e099f6f8519f4aea959e37381c54` |
| `T4-MR3-final.json` | `07a28bae-85fb-4da7-99b7-dfef08289351::local.ehrbase.org::1` | 0 | `5b39ee1bae185ba8da28e339d83bbde64cd5b9594c083a70bb0cf70fee2c8454` |
| `T4-MR4-final.json` | `115c09a9-622d-43f3-91d5-dbff7af0ec79::local.ehrbase.org::1` | 0 | `e5c7f14b917be9215eba5ff685bdde87db981ea1cf6e71aeb1325d8fe0baa894` |
| `T4-MR6-final.json` | `9e9a8965-367a-4bbb-9279-7a223b5fa811::local.ehrbase.org::1` | 0 | `be2a629fb6baa99e08b8e28c84bcdbbf97b9f7a219e0acc562bf7780ca7d8a68` |
| `T4-MR7-final.json` | `6b0ec61c-37d1-4bc5-a239-cde980469ee2::local.ehrbase.org::1` | 0 | `5e23f0d73cec8b373affb0ad75e0d2014310562e18db30194f35f6a77c13c46d` |
| `T4-MR8-final.json` | `8bb59241-2eda-42a2-9399-276a0f452f6a::local.ehrbase.org::1` | 0 | `3ac272a5ecfd313faa13007221f1e2585fde9677f95af68670cac2ccbc6f88a1` |
| `T4-MR9-final.json` | `6d7c00cb-b738-4975-b38e-7b5e2eb2575d::local.ehrbase.org::1` | 0 | `90a7fe9bb0665f4d494072f15ba41d2e4b545f8f84d80ab8be23c49472c9ecf8` |
| `T4-CE2-get-response-v1.json` | `ebe7f166-85c0-4c68-bf8a-572f32cc2c3c::local.ehrbase.org::1` | 0 | `043858502269732ba76d423fca77e214ea967740dca00d3d5147149bcc898213` |

Archive totals: Nine final MR versions, two final CE versions, four final EP versions, and one historical CE2 version, yielding 16 JSON files representing 15 logical COMPOSITIONs. Of the 33 references, CE1 contains five, final CE2 `::2` contains four, and EP1–EP4 contain 7 + 12 + 2 + 3 = 24. Historical CE2 `::1` has no relationship CLUSTER. The archived MR5 filename is `T4-MR5-final.json`.

## Other Observations Recorded in the Interactive Test Session

- Nine MR POST responses with HTTP 201 and independent GET responses with HTTP 200 were recorded in the interactive test session. The original T4-specific MR POST request payloads are not included in the archived `requests.zip`.
- CE1/CE2/EP1–EP4 REST status codes and GET results were recorded in the test session. The 16 archived JSON bodies provide independently inspectable content evidence, but not original HTTP response headers or status logs.
- AQL results were recorded in the interactive test session, including 15 final COMPOSITIONs, nine CE references, 24 EP references, 25 ENTRYs, 19 clinical MR ENTRYs, 12 EP2 references, and SOAP and diagnosis queries. Original Postman AQL response exports are not included.
- The archived historical CE2 `::1` export lacks the relationship CLUSTER, whereas final CE2 `::2` contains four CE-to-MR references. This supports the documented versioned update and retention observations.

## Remaining Archive Limitations

A more complete independent audit would require the original MR1–MR9 POST payloads, AQL request/response pairs, and REST status headers or Postman collection logs. Their absence limits archive completeness but does not establish test failure. Neither the stored `DV_EHR_URI` values nor the offline content checks demonstrate native dereferencing, referential-integrity enforcement, or validation of all ENTRY-level target paths. Historical byte-for-byte equivalence with the original execution artifacts has not been independently verified.
