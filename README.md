# Terraform Google Secret
A terraform module to create google secrets


## Usage

```hcl
locals {
  secrets = {
    "database-credentials" = jsonencode({
      "user"     = local.db_user_name
      "password" = random_id.this.hex
      "host"     = random_id.this.id
      "name" = local.db_name
    })
    token = "XYZ"
  }
}

module "google_secrets" {
  for_each = local.secrets
  source   = "git::ssh://git@gitlab.com/deimosdev/tooling/terraform-modules/gcp/terraform-google-secret.git"
  id       = each.key
  value    = each.value
  labels   = local.common_labels
}

```

## Doc generation

Code formatting and documentation for variables and outputs is generated using [pre-commit-terraform hooks](https://github.com/antonbabenko/pre-commit-terraform) which uses [terraform-docs](https://github.com/segmentio/terraform-docs).


And install `terraform-docs` with
```bash
go get github.com/segmentio/terraform-docs
```
or
```bash
brew install terraform-docs.
```

## Contributing

Report issues/questions/feature requests on in the issues section.

Full contributing guidelines are covered [here](CONTRIBUTING.md).

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.12.26 |
| google | >= 3.29 |

## Providers

| Name | Version |
|------|---------|
| google | >= 3.29 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| id | (Required) This must be unique within the project. | `any` | n/a | yes |
| labels | (Optional) The labels assigned to this Secret | `map` | `{}` | no |
| value | (Required) The secret data. Must be no larger than 64KiB. Note: This property is sensitive and will not be displayed in the plan. | `any` | n/a | yes |

## Outputs

No output.

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
