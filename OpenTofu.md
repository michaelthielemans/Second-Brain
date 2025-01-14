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
# apply the configuratio to the real infrastructure
tofu apply
```

```
# show the resources that are in the state file
tofu show

# show the content of the statefile (json)
tofu state list
```

```
tofu destroy
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

##### Auto approve commands
```bash
tofu <command> -auto-approve
```

##### Outputs
You can show some outputs that will be shown at the end when the terraform apply procedure is finished.
```HCL
output websiteurl {
  value = aws_s3_bucket_website_configuration.<your-initials>website.website_endpoint
}
```


After the `tofu apply`, you can also use `tofu output <name-of-attribute>` to get the value of one specific attribute.
```bash
$tofu output websiteurl
"s3website.bv.bucket.s3-website-us-east-1.amazonaws.com"
```
## Modules
A directory with different .ft files is called a directory


