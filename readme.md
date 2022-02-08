# Terraform module for AWS SSO

This is a module for AWS SSO which grants given permission to SSO group and assigns given accounts to it.

For example the snippet below grants permission `arn:aws:iam::aws:policy/AlexaForBusinessDeviceSetup` to `AlexaUsers` group (created manually in AWS SSO, because there is no AWS API for this operation) and assigns AWS accounts `001000000998` and `001000000999` to that group.   

```hcl
module "sso_admins" {
  source = "github.com/hekonsek/terraform-aws-sso"

  name = "AlexaUsers"
  policy_arn = "arn:aws:iam::aws:policy/AlexaForBusinessDeviceSetup"
  accounts = [
    "001000000998", "001000000999"
  ]
}
```

The default permission for the group is `arn:aws:iam::aws:policy/AdministratorAccess` , so you can assign administrators to your AWS accounts just like that:

```hcl
module "sso_admins" {
  source = "github.com/hekonsek/terraform-aws-sso"

  name = "Administators"
  accounts = [
    "001000000998", "001000000999"
  ]
}
```

<!-- BEGIN_TF_DOCS -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_ssoadmin_account_assignment.assignment](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_account_assignment) | resource |
| [aws_ssoadmin_managed_policy_attachment.permissionset_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_managed_policy_attachment) | resource |
| [aws_ssoadmin_permission_set.permissionset](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_permission_set) | resource |
| [aws_identitystore_group.groups](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/identitystore_group) | data source |
| [aws_ssoadmin_instances.ssos](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/ssoadmin_instances) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_accounts"></a> [accounts](#input\_accounts) | n/a | `set(string)` | n/a | yes |
| <a name="input_name"></a> [name](#input\_name) | n/a | `any` | n/a | yes |
| <a name="input_policy_arn"></a> [policy\_arn](#input\_policy\_arn) | n/a | `string` | `"arn:aws:iam::aws:policy/AdministratorAccess"` | no |

## Outputs

No outputs.
<!-- END_TF_DOCS -->

## License

This project is distributed under [Apache 2.0 license](http://www.apache.org/licenses/LICENSE-2.0.html).