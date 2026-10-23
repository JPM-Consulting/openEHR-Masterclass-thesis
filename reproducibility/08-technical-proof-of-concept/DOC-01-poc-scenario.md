# PoC Scenario

**Status:** Clinical reference scenario used for the technical proof of concept (T0–T5). This document defines the synthetic case and modeling assumptions. Execution outcomes and remaining limitations are recorded separately in [PoC Results](DOC-04-poc-results.md).

## Synthetic Patient Medical History

The synthetic patient has a history of arterial hypertension, diagnosed in 2009, and WHO grade I obesity. Both conditions are considered active and form part of the patient’s longitudinal medical record.

The clinical scenario covers two outpatient consultations on November 15 and November 17, 2024, primarily related to an acute urinary tract infection.

### First Consultation: November 15, 2024

The patient presents with a three-day history of dysuria (burning sensation during urination). This is the first reported episode of urinary symptoms. The patient denies visible blood in the urine.

Vital signs and body measurements are recorded during the initial consultation. Blood pressure is 140/90 mmHg, with a heart rate of 75 beats per minute. The patient weighs 86 kg and is 168 cm tall, with a documented body mass index (BMI) of 30.5 kg/m².

A urine dipstick analysis reveals leukocyte esterase 3+, positive nitrites, blood 1+, trace protein, and a urinary pH of 6.0. These findings, together with the patient’s symptoms and the presence of pyuria, support the initial clinical assessment of suspected cystitis.

The consultation is documented in a structured SOAP progress note. The subjective findings describe the urinary symptoms, while the objective findings include pyuria. The assessment identifies suspected cystitis. The treatment plan includes microbiological investigation with an antibiogram and initiation of empirical antimicrobial therapy.

The patient is prescribed oral trimethoprim–sulfamethoxazole (160 mg trimethoprim / 800 mg sulfamethoxazole), one tablet twice daily.

In addition to the acute urinary tract infection, the patient’s existing arterial hypertension and obesity remain active health problems.

### Second Consultation: November 17, 2024

The patient returns for follow-up. Urinary symptoms are still present despite the antimicrobial treatment initiated two days earlier.

The urine culture and susceptibility testing identify *Escherichia coli* at a concentration of at least 10⁵ CFU/mL. Antimicrobial susceptibility testing demonstrates resistance to trimethoprim–sulfamethoxazole and ciprofloxacin. The organism remains susceptible to amoxicillin–clavulanate, nitrofurantoin, and fosfomycin.

Repeat vital signs show a blood pressure of 142/85 mmHg and a heart rate of 72 beats per minute.

The follow-up SOAP progress note records persistent urinary symptoms and the microbiological evidence of resistance to the initially prescribed antibiotic. Based on these findings, the clinical assessment is updated from suspected cystitis to acute bacterial cystitis.

The treatment plan is revised. The initial antimicrobial therapy is replaced with oral amoxicillin–clavulanate (500 mg amoxicillin / 125 mg clavulanate), one tablet three times daily.

The urinary tract infection remains an active health problem, while the patient’s pre-existing arterial hypertension and obesity continue to be documented as active conditions.

### Longitudinal Clinical Context

The synthetic medical history illustrates the management of an acute urinary tract infection across two outpatient consultations.

The initial consultation establishes the presenting symptoms, diagnostic findings, provisional clinical assessment, and empirical antimicrobial treatment. The follow-up consultation provides additional microbiological evidence, leading to refinement of the clinical assessment and modification of antimicrobial therapy.

Throughout this sequence, the urinary tract infection represents a single longitudinal clinical problem whose documentation evolves over time.

The patient’s arterial hypertension and obesity provide additional longitudinal clinical context. Vital signs are recorded during both consultations and may be clinically relevant to these pre-existing conditions.

The scenario combines an evolving acute health problem, persistent chronic conditions, and repeated clinical observations.

## Clinical Data Modeling and Template Constraints

The openEHR templates used in this technical proof of concept (PoC) were designed to include only the clinical data elements needed to represent the synthetic patient scenario. The PoC investigates the technical representation, persistence, and retrieval of relationships between Care Encounters, Episodes of Care, and Medical Record Entries. Comprehensive clinical documentation and terminology interoperability are outside its scope.

The templates retain all mandatory data elements defined by the underlying openEHR archetypes and selected optional elements required for the clinical scenario. Optional elements outside the PoC scope were excluded through template-level constraints, using occurrences of `0..0` where permitted. The original international CKM archetypes were not modified.

Clinical terminology coding was minimized. Where supported by the underlying archetypes, diagnoses, medication names, and other descriptive concepts are represented using `DV_TEXT`, without terminology bindings or additional coding. Existing coded values and value sets defined by the CKM archetypes were retained without modification. Structured data types, including `DV_QUANTITY`, `DV_DATE_TIME`, and `DV_CODED_TEXT`, were preserved wherever required by the openEHR Reference Model or archetype constraints.

Two variants of each relevant template were created for the evaluation of the three implementation patterns. The FOLDER and LINK patterns share templates without embedded Episode-of-Care relationship structures, whereas the CLUSTER pattern uses separate template variants incorporating archetyped relationship information. This design supports representation of the same clinical information across all three patterns while allowing their relationship mechanisms to be examined separately.

The resulting templates are research-specific artifacts intended for this technical PoC. They are not designed to serve as comprehensive clinical documentation models or production-ready implementation templates.

Clinical Section FOLDER-based organization is outside the PoC scope. Existing openEHR `SECTION` structures inside COMPOSITIONs, including the SOAP note section, remain part of the clinical templates.

## Templates

| ID | Template | Template ID |
| --- | --- | --- |
| TE01 | Care Encounter | `JPM_Care_Encounter.v1` |
| TE02 | Care Encounter – CLUSTER relationships | `JPM_Care_Encounter_Cluster.v1` |
| TE03 | Episode of Care | `JPM_Episode_of_Care.v1` |
| TE04 | Episode of Care – CLUSTER relationships | `JPM_Episode_of_Care_Cluster.v1` |
| TE05 | Medical Record Body Measurements | `JPM_Medical_Record_Body_Measurements.v1` |
| TE06 | Medical Record Body Measurements – CLUSTER relationships | `JPM_Medical_Record_Body_Measurements_Cluster.v1` |
| TE07 | Medical Record Medication Order | `JPM_Medical_Record_Medication_Order.v1` |
| TE08 | Medical Record Medication Order – CLUSTER relationships | `JPM_Medical_Record_Medication_Order_Cluster.v1` |
| TE09 | Medical Record Microbiology Result | `JPM_Medical_Record_Microbiology_Result.v1` |
| TE10 | Medical Record Microbiology Result – CLUSTER relationships | `JPM_Medical_Record_Microbiology_Result_Cluster.v1` |
| TE11 | Medical Record Urin Analysis | `JPM_Medical_Record_Urin_Analysis.v1` |
| TE12 | Medical Record Urin Analysis – CLUSTER relationships | `JPM_Medical_Record_Urin_Analysis_Cluster.v1` |
| TE13 | Medical Record Vital Signs | `JPM_Medical_Record_Vital_Signs.v1` |
| TE14 | Medical Record Vital Signs – CLUSTER relationships | `JPM_Medical_Record_Vital_Signs_Cluster.v1` |
| TE15 | SOAP Progress Note | `JPM_SOAP_Progress_Note.v1` |
| TE16 | SOAP Progress Note – CLUSTER relationships | `JPM_SOAP_Progress_Note_Cluster.v1` |

### Template Availability and Reproducibility

All 16 openEHR templates are provided in two formats: Operational Templates (OPT) and ZIP packages. The OPT files are intended for deployment to the openEHR Clinical Data Repository (CDR). The ZIP packages include the corresponding templates and required archetypes. The ZIP packages allow reviewers to import and inspect the clinical models in a compatible openEHR modeling environment without retrieving the archetypes separately.

The 16 OPT files and 16 ZIP packages are provided in `02-templates/opt/` and `02-templates/zip/`, respectively.

## Test Data

### Care Encounters

| ID | Date | Reason for Encounter |
| --- | --- | --- |
| CE1 | 2024-11-15 | Initial consultation for dysuria (chief complaint: burning sensation with urination) |
| CE2 | 2024-11-17 | Follow-up visit and chart completion |

### Episodes of Care

| ID | Name | Notes |
| --- | --- | --- |
| EP1 | General health problem | Default Episode of Care when no specific episode applies as the primary clinical context; not a parent episode |
| EP2 | Urinary tract infection | Acute health problem |
| EP3 | Arterial hypertension | Chronic diagnosis |
| EP4 | Obesity WHO grade I | Chronic diagnosis |

### Medical Record Entries: November 15, 2024

| ID | Template | Content |
| --- | --- | --- |
| MR1 | Medical Record Vital Signs | Systolic 140 mmHg; diastolic 90 mmHg; pulse 75/min |
| MR2 | Medical Record Body Measurements | Height 168 cm; weight 86 kg; documented BMI 30.5 kg/m² |
| MR3 | Medical Record Urin Analysis | Dipstick: leukocyte esterase 3+; nitrite positive; blood 1+; protein trace; pH 6.0 |
| MR4 | SOAP Progress Note | S: Burning sensation during urination for 3 days; first episode; denies visible blood in urine. O: Pyuria. A: Suspected cystitis. P: Antibiogram; start trimethoprim–sulfamethoxazole. |
| MR5 | Medical Record Medication Order | Trimethoprim–sulfamethoxazole (TMP 160 mg / SMX 800 mg), oral, one tablet twice daily |

### Medical Record Entries: November 17, 2024

| ID | Template | Content |
| --- | --- | --- |
| MR6 | Medical Record Microbiology Result | Urine culture: *Escherichia coli* ≥10⁵ CFU/mL; resistant to trimethoprim–sulfamethoxazole and ciprofloxacin; susceptible to amoxicillin–clavulanate, nitrofurantoin, and fosfomycin |
| MR7 | Medical Record Vital Signs | Systolic 142 mmHg; diastolic 85 mmHg; pulse 72/min |
| MR8 | SOAP Progress Note | S: Persistent urinary symptoms. O: Urine culture shows *E. coli* resistant to current antibiotic. A: Acute bacterial cystitis. P: Switch antimicrobial therapy. |
| MR9 | Medical Record Medication Order | Amoxicillin 500 mg / clavulanate 125 mg, oral, one tablet three times daily |

**Dataset provenance:** The synthetic case uses the documented weight of 86 kg and BMI of 30.5 kg/m² for MR2. The clinical scenario and its nine Medical Record COMPOSITIONs constitute the reference dataset for the documented PoC scenarios. The BMI value is reported as documented and has not been independently recalculated in this scenario specification.
