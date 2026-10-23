# LINK-Based Implementation Pattern

This directory contains two independently executed technical proof-of-concept (PoC) scenarios for representing Care Encounter and Episode of Care relationships with standard openEHR `LINK` objects. The scenarios differ in their creation sequence and relationship direction. Both use the same synthetic reference dataset and are documented separately.

## Test implementations

| Scenario | Documentation | Implementation and evidence |
|---|---|---|
| T2 | [T2 README](T2/README.md) | Clinical Medical Record COMPOSITIONs precede the context relationships. The archive contains 15 final COMPOSITION JSON exports and 10 request bodies. |
| T3 | [T3 README](T3/README.md) | Care Encounter and Episode of Care COMPOSITIONs precede the clinical Medical Record COMPOSITIONs. The archive contains 15 final COMPOSITION JSON exports and nine Medical Record request bodies. |

## Scope and evidence

Both scenarios represent Care Encounter-to-COMPOSITION and Episode of Care-to-ENTRY relationships without duplicating clinical ENTRY content. In each scenario, the documented final state comprises 15 COMPOSITIONs (nine Medical Records, two Care Encounters, and four Episodes of Care), 19 technical clinical ENTRYs, and 33 `LINK` instances. The 33 technical links represent 27 logical clinical relationships because two SOAP notes each contain four technical ENTRYs but constitute one clinical unit.

T2 and T3 have separate execution records, identifiers, and evidence limitations. For details, see the [T2 implementation](T2/T2-link-implementation.md), [T2 verification record](T2/T2-link-test-identifiers.md), [T3 implementation](T3/T3-link-implementation.md), and [T3 test results](T3/T3-link-test-results.md).

The documented tests demonstrate persistence and AQL retrieval of stored relationship metadata, as well as selective retrieval of referenced clinical content. T2 additionally documents manual assembly of an EP2 clinical view. Neither scenario demonstrates native `ehr://` target dereferencing, automatic end-to-end clinical view construction, or repository-enforced relationship invariants. These results should not be interpreted as a systematic execution of all eight clinician-centered user stories.
