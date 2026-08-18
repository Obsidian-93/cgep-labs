# cgep-labs

Lab work and evidence for the GRC Engineering Club's **CGE-P (Certified GRC Engineer, Practitioner)** certification.

This repo follows the program's compliance-as-code philosophy: every lab produces working infrastructure, evidence, and documentation, no screenshots. Code lives under `terraform/`, machine-readable evidence lives under `evidence/lab-X-Y/`, kept separate so either can be reviewed independently.

## Labs

| Lab | Topic | Code | Evidence |
|---|---|---|---|
| 2.3 | Compliant S3 bucket (NIST 800-53: SC-28, CM-6, AC-3, AU-3, AU-6) | [`terraform/primitives/compliant-s3`](terraform/primitives/compliant-s3) | [`evidence/lab-2-3`](evidence/lab-2-3) |

More labs added as the program progresses.
