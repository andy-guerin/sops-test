# sops-test

Used for SOP related codefresh pipeline testing

The `.sops.yaml` file allows creation rules to be defined when creating encrypted files.

For example the following configuration ensures that any files created in the secrets folder using `sops` CLI will automatically be encrypted using the GCP KMS key defined in the configuration. Similarly AWS, Azure KMS or PGP can be used.

This is good for secret authors as they don't need to run `gcloud kms encrypt...`

An author will need to authenticate with GCP using 
`gcloud auth application-default login`
ro  enable application default credentials which SOPS uses by default for GCP KMS

```yaml
creation_rules:
  - path_regex: .*/secrets/*
    gcp_kms: projects/company-ex-dev/locations/australia-southeast1/keyRings/dept-keyring/cryptoKeys/app-key
```

