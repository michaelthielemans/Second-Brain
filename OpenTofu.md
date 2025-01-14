#### Common commands:
```
# check version
tofu -v
```

```
# initialize 
tofu init
```
The `terraform init` phase sets up everything necessary for Terraform to interact with your infrastructure. It ensures that providers, modules, and backends are properly initialized, and it makes the environment ready for applying infrastructure changes.

```
tofu plan
```
When triggering the plan command terraform will first check if the statefile is up to date with the read world infrastructure. I executes a tofu refresh in the background. If the state file is refreshed it then can calculate the difference between the configured configuration you have written in the terraform files and the statefile.



```

tofu apply
```
```
# show the resources that are in the state file
tofu show

# show the content of the statefile (json)
tofu state list
```


## HCL - terraform files .tf
Hashicorp Configuration Language

#### Different kind of files:

***Terraform state file (backend)***
	terraform.tfstate in json format


## Tips
##### Versioning:
when specifying a provider it is best practice to define a version. So you have a version restriction in order to prevent breaking changes.

##### Variables
environment variables and terraform/opentofu.
create TF_VAR_ example so terraform can read it. -> var.example




## Modules
A directory with different .ft files is called a directory


