# T3 — LINK Pattern: Care Encounters and Episodes of Care First

**Status:** Completed, with passing results within the documented test scope (EHRbase 2.30.1, REST canonical JSON, AQL, Postman).  
**Isolated EHR:** `f4908498-afef-4e3c-8cc4-bbdf16d808bf`. **System:** `local.ehrbase.org`. **RM:** 1.0.4.

## Files

- [`T3-link-implementation.md`](T3-link-implementation.md): architecture, creation sequence, relationship roles, and clinical modeling decisions.
- [`T3-link-test-identifiers.md`](T3-link-test-identifiers.md): versioned identifiers and the relationship inventory.
- [`T3-link-test-results.md`](T3-link-test-results.md): execution log T3.1–T3.7, observed results, errors, and limitations.
- [`T3-aql-query-catalog.md`](T3-aql-query-catalog.md): AQL statements, expected results, and corrected variants, including reconstructed queries where original requests were not retained.
- [`T3-evidence-manifest.md`](T3-evidence-manifest.md): evidence inventory and provenance limitations, distinguishing archived request payloads from server GET exports.
- [`json/requests/`](json/requests/): nine pre-submission canonical JSON request bodies, not independently retrieved server responses.

## Outcome

The documented T3 execution comprises 15 COMPOSITIONs (2 Care Encounters, 4 Episodes of Care, and 9 Medical Records) and 19 technical ENTRYs. Nine encounter LINKs, 19 primary episode LINKs, and five associated episode LINKs total 33 technical LINK instances. All nine Medical Record COMPOSITIONs were individually inspected as returned JSON, and all 33 LINK instances were queried using AQL. The documented EP2 retrieval identifies 12 ENTRYs in six Medical Record COMPOSITIONs across CE1 and CE2. EP3 identifies two associated blood-pressure observations, and EP4 identifies three associated body measurements.

**Evidence boundary:** Stored `DV_EHR_URI` values were queried and interpreted at the application level. Native target dereferencing, automatic clinical-view reconstruction, and server-side enforcement of role, uniqueness, and referential-integrity constraints were not demonstrated. The eight clinician-centered user stories and six architectural criteria were not systematically tested as part of T3.

## Archived JSON Exports

- [`json/requests/`](json/requests/): nine Medical Record POST request bodies (MR1–MR9). These are input payloads, not GET-response evidence.
- [`json/persisted/`](json/persisted/): 15 archived final COMPOSITION JSON exports (CE1–CE2, EP1–EP4, MR1–MR9), each containing a versioned UID.
- The export inventory and SHA-256 checksums are recorded in [`T3-evidence-manifest.md`](T3-evidence-manifest.md).

**AQL evidence:** Retrieval queries, including reconstructed query templates where original request payloads were not retained, are documented in [`T3-aql-query-catalog.md`](T3-aql-query-catalog.md). Observed outcomes are recorded in [`T3-link-test-results.md`](T3-link-test-results.md). Complete AQL response payloads were not separately archived.
