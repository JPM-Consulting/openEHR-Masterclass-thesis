# T1 — Evidence and Provenance Manifest

## Archive inventory

This manifest inventories the archived evidence files for the T1 Basic FOLDER scenario. It does not document a new test execution.

- Four DIRECTORY request JSON payloads in `tests/`.
- Sixteen JSON exports in `json/persisted/`: 15 COMPOSITIONs (CE1–CE2, EP1–EP4, MR1–MR9) and one DIRECTORY export.
- One supplementary Markdown file containing test identifiers (excluding `README.md`).

## DIRECTORY request payloads

| Relative path | SHA-256 |
| --- | --- |
| `tests/T1.3-directory-initial-POST.json` | `f4d683530b8922929315e1c1ee3041bcf7fca9bbb06e0a287e1fe061e07e3ded` |
| `tests/T1.6-directory-add-relationship-from-v1-PUT.json` | `3bb7d74a59bc939661e90a88c1be5d501a2a600eb67e05c71447b834da4f5c6c` |
| `tests/T1.6-directory-add-relationship-from-v2-PUT.json` | `9a0c73580278fad05256ff104a899d39d6a229c266e8eed167041a254b0130f7` |
| `tests/T1.7-directory-remove-relationship-from-v3-PUT.json` | `a27cecd6db760437d3b2957a38c898adc02031d0d6c1bcd23ba2f13f0f42b590` |

The request payloads record submitted or prepared DIRECTORY states. A payload alone does not establish a successful server response. See [the T1 README](README.md) and [the test identifiers](T1-basic-folder-test-identifiers.md) for the documented sequence and limitations.

## Persisted JSON exports

| Relative path | UID in JSON (where available) | SHA-256 |
| --- | --- | --- |
| `json/persisted/T1-CE1-final.json` | `7d94b831-a3f9-4dcc-9357-76017c798de1::local.ehrbase.org::1` | `fe6ed5c75914511ca1f7fb11c9228e104b5554c27f82b6b4ab5c93ebdeaed155` |
| `json/persisted/T1-CE2-final.json` | `7fe11fce-0f8f-496f-b947-7c545a59bfb4::local.ehrbase.org::1` | `fa5b9fb60dd26bd95f62db63bc36a62d6ff2146875088d72489c862e774e5a39` |
| `json/persisted/T1-DIRECTORY-basic-final.json` | `7961df16-9674-4959-8048-ea016c48dfcb::local.ehrbase.org::4` | `367a9e97b9c9ff5780a719455fbc2cfa6e918209310e7e1cc2bfba4cb00e1413` |
| `json/persisted/T1-EP1-final.json` | `e6746cc1-372c-4a95-b078-51b66f50b1b1::local.ehrbase.org::1` | `f420e8052af96ff20c0d1075ed0f8cb90ad63f73908695addc12273a20c33526` |
| `json/persisted/T1-EP2-final.json` | `5d96fcf0-5988-4649-a70b-0b05b4f89133::local.ehrbase.org::1` | `67cf13026f4313d14ce7a936247e053ec534f27a49bff8e106c13bd4099d1b89` |
| `json/persisted/T1-EP3-final.json` | `99ebe958-d9a9-4fd0-ac49-ca0b2db241f0::local.ehrbase.org::1` | `3c3105831823ab0259466fe52bf9c26e7695067a03ba3648891ddbc085d50083` |
| `json/persisted/T1-EP4-final.json` | `e0df43fe-f506-47ad-90ec-3e5a480cb5f5::local.ehrbase.org::1` | `44ad76eee761e6eb2d73301d525274618032c88182914c6e95843f4d48ca3534` |
| `json/persisted/T1-MR1-final.json` | `a5b1e471-f28f-4365-b0b0-51c1fb03b112::local.ehrbase.org::1` | `7eccaea4223d845882ea58e3bad6a52656db6292e3b33e017fe7bad707f0add3` |
| `json/persisted/T1-MR2-final.json` | `93e1160d-c364-4cb5-b15b-5a12ab6a5024::local.ehrbase.org::1` | `7fe63cb40b23a869878bf43581a033da84ba6014c6eb7c41e3f0b12838336479` |
| `json/persisted/T1-MR3-final.json` | `6a93d5f8-78b5-4df0-b699-5b3580d6112b::local.ehrbase.org::1` | `ad8a51564993c8bbff66c6009761f1403af95b94b0fdf62d6ae6fe468d1451cd` |
| `json/persisted/T1-MR4-final.json` | `d524a132-ea78-41a8-b112-10a2ed795ea4::local.ehrbase.org::1` | `d15fe53e516c6ac5556f03b70ecae73f089fe39177f6f0fbeb185dfcab8db9a8` |
| `json/persisted/T1-MR5-final.json` | `a731f2a6-cd0c-4386-a419-ff872889d9d1::local.ehrbase.org::1` | `b927a4d6bad087eb5341de031e5b356c2524b7912f4d42f60006b1d973c3f58a` |
| `json/persisted/T1-MR6-final.json` | `3ffb2e64-1a13-4adf-94c3-e050ceaa609b::local.ehrbase.org::1` | `47fbbf375a058acd4b311598d98d50c14e52c7c4f9247594074ea3c27ee9313f` |
| `json/persisted/T1-MR7-final.json` | `983478c2-1060-4fc8-b534-7eb7ed6cee6a::local.ehrbase.org::1` | `96a9688bf1f9227656bba38b1d8cd4a7d9f5c1e038233f259c2eede43d986c69` |
| `json/persisted/T1-MR8-final.json` | `efc0672a-51b9-4722-99b1-bb4d92b0a8cd::local.ehrbase.org::1` | `c3f06bea2a781c439b5168997f30510af8949537fcfddb3e7e8c0da0c35120f6` |
| `json/persisted/T1-MR9-final.json` | `4df8bcde-5b89-4df4-b47b-1eb7080dad9d::local.ehrbase.org::1` | `d5896b4f90d8a221f9e9ec03868a3c9ef8ff0e2eb2fc5020a1e583b00d752ea2` |

## Supporting documentation

| Relative path | SHA-256 |
| --- | --- |
| `T1-basic-folder-test-identifiers.md` | `d96fd2ad6262a3e82dd6c83bdf6a974918eb036990d30c4d68b1f43627d0cbff` |

## Evidence scope and limitations

- SHA-256 hashes identify the exact archived file bytes and support integrity checks. They do not independently establish when or how REST requests were executed.
- The 15 COMPOSITION JSON exports and one DIRECTORY export document archived data states. The DIRECTORY export does not establish the contents of every intermediate DIRECTORY version.
- Selected AQL retrieval observations are recorded in the test documentation. Complete AQL response payloads are not separately archived in this T1 directory.
- Native automatic `DV_EHR_URI` dereferencing and systematic execution of all eight clinician-centred views were not demonstrated in T1.
- The observed intermediate DIRECTORY PUT error and uncertainty about response attribution remain as described in the scenario README and supporting test documentation.

## Integrity verification

When this manifest was prepared, all listed JSON files were successfully parsed from the original archive and their checksums were calculated from the archived bytes. No source artifacts or tests were modified.
