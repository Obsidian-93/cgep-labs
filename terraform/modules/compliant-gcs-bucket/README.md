# compliant-gcs-bucket

A reusable Terraform module that provisions a GCS bucket with a hardened security baseline locked inside it. Consumers can choose business settings like environment and retention period; they cannot choose to turn off encryption, versioning, or public access prevention, because those choices were never exposed through the module's interface.

| Control | What it means | Where it's enforced |
|---|---|---|
| SC-12 | The organization establishes and owns the cryptographic key, rather than relying on a provider-managed default | `google_kms_key_ring` + `google_kms_crypto_key` |
| SC-13 / SC-28 | Data at rest is protected with a customer-managed encryption key (CMEK) that rotates on a fixed schedule | `encryption {}` block on the bucket, `rotation_period = "7776000s"` on the key |
| AC-3 | Access is enforced uniformly at the bucket level and the bucket can never be made publicly reachable | `uniform_bucket_level_access = true`, `public_access_prevention = "enforced"` |
| AU-11 | Objects are retained for a defined period appropriate to the environment (30 days minimum for dev, 365 days minimum for prod) | `retention_policy {}` block, environment-aware validation in `variables.tf` |
| CM-6 | Every bucket carries a required set of compliance labels that a consumer can add to but cannot remove or override | `local.effective_labels = merge(var.labels, local.required_labels)` |

Two consumers, `compliant-gcs` (dev) and `compliant-gcs-prod` (prod), call this module with different business settings and inherit the identical security posture. A third, `compliant-gcs-negative`, deliberately violates the prod retention rule to demonstrate that `terraform plan` catches the violation before any resource is created.
