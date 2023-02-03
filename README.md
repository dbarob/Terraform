# simple-azure-blob

Terraform Module to Create Azure Blob Storage

## Usage

```terraform
variable "resource_group_name" {}
variable "storage_account_name" {}

#####################################################################
## Create Resource Group, Storage Account Name
#####################################################################
module "app_backups" {
  source                  = "git::https://github.com/darkn3rd/simple-azure-blob?ref=v0.1"
  resource_group_name     = var.resource_group_name
  create_resource_group   = true
  storage_account_name    = var.storage_account_name
  create_storage_account  = true
  storage_container_name  = "app-backups"
}

#####################################################################
## Create ONLY Blob
#####################################################################
module "data_backups" {
  source                  = "git::https://github.com/darkn3rd/simple-azure-blob?ref=v0.1"
  resource_group_name     = module.app_backups.ResourceName
  create_resource_group   = false
  storage_account_name    = module.app_backups.AccountName
  create_storage_account  = false
  storage_container_name  = "data-backups"
}
```
