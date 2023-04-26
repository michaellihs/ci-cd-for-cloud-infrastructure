# CI/CD pipelines for cloud infrastructure

This is an accompanying repository with a sample implementation of the principles of the "CI/CD pipelines for cloud infrastructure" presentation by [Waldemar Kindler](https://www.github.com/kindlertw) and [Michael Lihs](https://www.github.com/michaellihs).

The foundations are shamelessly copied from the [terraform-workspaces-terragrunt-ansible repository](https://github.com/neilpricetw/terraform-workspaces-terragrunt-ansible) by [Neil Price](https://github.com/neilpricetw).

## Prerequisites

- install the `awscli`

   ```shell
   brew install awscli
   ```

## Creating and destroying the environments

### Locally

```
terraform init -backend=false
```

### Dev 
```
terraform init -backend-config=config.dev.tfbackend
terraform plan -var-file=terraform-dev.tfvars -var-file=non-prod.tfvars
terraform apply -var-file=terraform-dev.tfvars -var-file=non-prod.tfvars -auto-approve

terraform destroy -var-file=terraform-dev.tfvars -var-file=non-prod.tfvars -auto-approve
```

### Test
```
terraform init -backend-config=config.test.tfbackend
terraform plan -var-file=terraform-test.tfvars -var-file=non-prod.tfvars
terraform apply -var-file=terraform-test.tfvars -var-file=non-prod.tfvars -auto-approve

terraform destroy -var-file=terraform-test.tfvars -var-file=non-prod.tfvars -auto-approve
```

### Staging
```
terraform init -backend-config=config.staging.tfbackend
terraform plan -var-file=terraform-staging.tfvars -var-file=non-prod.tfvars
terraform apply -var-file=terraform-staging.tfvars -var-file=non-prod.tfvars -auto-approve

terraform destroy -var-file=terraform-staging.tfvars -var-file=non-prod.tfvars -auto-approve
```

### Prod
```
terraform init -backend-config=config.prod.tfbackend
terraform plan -var-file=terraform-prod.tfvars
terraform apply -var-file=terraform-prod.tfvars -auto-approve

terraform destroy -var-file=terraform-prod.tfvars -auto-approve
```

## TODOs

- [ ] provide an explanation of the directory structure in README
- [ ] introduce boostrapping script (`./do.sh`)
- [ ] introduce pipeline
- [ ] introduce testing & linting tools as mentioned in the presentation
