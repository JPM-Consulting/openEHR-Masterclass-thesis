# EHRCON26 Conference Material

This directory contains material associated with the presentation of the study at EHRCON26:

- `ehrcon26-poster.pdf`: Conference poster.
- `ehrcon26-5min-presentation.pdf`: Slides for the five-minute conference presentation.

These materials summarize the study as presented at the conference, including the conceptual model, the three openEHR implementation patterns, and the resulting design considerations.

The files are preserved as **historical conference artifacts** to document the development and communication of the research. They provide contextual and provenance information but do **not** constitute independent evidence for the functional or architectural evaluation in the current study.

## Clarification of the Medical Record Entry Count

The original EHRCON26 conference materials reported **132 clinical entries** in the synthetic longitudinal patient history. Subsequent verification of the underlying dataset established that it contains **121 Medical Record Entries**. The earlier total included 11 blank separator rows between Care Encounters that are not clinical Medical Record Entries.

The current manuscript and reproducibility package consistently use the verified count of **121 Medical Record Entries**. The historical conference files remain unchanged to preserve the original record of what was presented. This README documents the discrepancy and its resolution.

## Relationship to the Current Study

The conference materials reflect an earlier stage of the research. The current manuscript and the corresponding reproducibility artifacts, including the conceptual, functional, architectural, and technical proof-of-concept documentation, provide the reference basis for the final study design, evaluation, results, and conclusions.

Where the historical conference materials differ from the current study, the current manuscript and its supporting reproducibility evidence take precedence.
