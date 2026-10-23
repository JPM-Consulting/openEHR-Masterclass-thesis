# T5: CLUSTER-Based Clinical ENTRY to Care Encounter and Episode of Care

Status: Completed, with passing results within the documented test scope (21 October 2026).  
System: EHRbase 2.30.1, `local.ehrbase.org`, EHR `16fe2926-c82a-462c-93f2-d5e67a29656f`.  
Scope: 15 original COMPOSITIONs (2 Care Encounters, 4 Episodes of Care, and 9 Medical Records). A separate referential-integrity negative-test COMPOSITION increases the archived live-EHR total to 16.  
Design: The relationship CLUSTER `openEHR-EHR-CLUSTER.eoc_relationships_entry.v0` is embedded in the `protocol` of each clinical ENTRY. Stored `DV_EHR_URI` values reference versioned Care-Encounter and Episode-of-Care COMPOSITIONs. Episode roles are `Primary` (`at0154`) and `Associated` (`at0155`). The Care-Encounter and Episode-of-Care COMPOSITIONs do not contain reciprocal T5 relationship CLUSTERs.

## Contents

- [Implementation and modeling](T5-cluster-implementation.md)
- [Identifiers and test dataset](T5-cluster-test-identifiers.md)
- [Test results](T5-cluster-test-results.md)
- [AQL query catalog](T5-aql-query-catalog.md)
- [Evidence manifest](T5-evidence-manifest.md)
- `json/requests/`: Archived MR1–MR9 POST request payloads and the RI-02 request, checked against the uploaded local files.
- `json/aql/`: AQL request bodies reconstructed from queries documented during the test session. These are reproduction artifacts, not necessarily byte-identical copies of the original requests.
- `json/persisted/`: 16 archived COMPOSITION JSON files retrieved by REST GET at the end of the documented T5 execution, comprising 15 original COMPOSITIONs and one RI-02 negative-test COMPOSITION.

## Findings

- All 15 original COMPOSITIONs were independently retrieved after POST. They contain 19 technical clinical ENTRYs.
- The original dataset contains 33 logical clinical relationships: 9 Medical-Record-to-Care-Encounter and 24 clinical-ENTRY-to-Episode-of-Care relationships (19 Primary and 5 Associated). These are represented by 43 stored `DV_EHR_URI` occurrences (19 Care Encounter and 24 Episode of Care), reflecting ENTRY-level representation of the SOAP notes.
- AQL-01–AQL-12 were reported as PASS within the documented test scope. The EP2 longitudinal SOAP view was assembled from MR4 and MR8, with four technical SOAP ENTRYs per clinical note. Each SOAP note remains one clinical unit.
- Independent retrieval of EP2 by GET was successful. This does not demonstrate automatic URI dereferencing.
- RI-01–RI-04 documented negative-test execution. In the tested EHRbase configuration, a COMPOSITION containing a reference to a nonexistent Episode of Care was accepted, retrieved, and queried. This observation does not establish the behavior of other openEHR repositories or configurations.
- Production governance requirements and other test-scope limitations are documented in the linked implementation and results files.

The RI test added a tenth Medical Record COMPOSITION (`056c6620-67b0-408f-bf90-1f8458fe8b66::local.ehrbase.org::1`) containing a dangling Episode-of-Care URI. Exclude this additional test COMPOSITION from original dataset counts and unrestricted AQL inventory comparisons.

## Evidence boundary

The AQL queries and recorded retrieval results are documented in [the AQL query catalog](T5-aql-query-catalog.md) and [the test results](T5-cluster-test-results.md). Complete AQL response payloads were not separately archived. The reported tests demonstrate persistence and selective retrieval within the documented environment, not automatic end-to-end reconstruction of all clinician-centered views or server-side enforcement of all relationship constraints.
