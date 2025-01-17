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
When triggering the plan command terraform will first check if the statefile is up to date with the read world infrastructure. I executes a tofu refresh in the background. If the state file is refreshed it then can calculate the difference between the declared configuration in the terraform files you have written  and the tf.statefile.

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
## State file terraform.tfstate
### Key Concepts of the Terraform State File

1. **Purpose of the State File:**
    
    - **Tracks Resource Metadata:**
        - The state file stores details about all the resources Terraform manages, including their current attributes, dependencies, and relationships.
    - **Determines Changes:**
        - Terraform compares the state file with the configuration and the actual infrastructure to calculate the "plan" for updates, creations, or deletions.
    - **Enables Resource Dependencies:**
        - Tracks dependencies between resources to ensure Terraform applies them in the correct order.
2. **State File Format:**
    
    - The state file is a JSON-formatted file (e.g., `terraform.tfstate`), but it is typically managed automatically by Terraform and should not be edited manually.
3. **Local vs. Remote State:**
    
    - By default, the state file is stored locally in the Terraform working directory.
    - For collaboration, remote backends (e.g., S3, Azure Blob, Terraform Cloud) are used to store the state file securely and share it among team members.

### Key Operations Related to the State File

1. **Initialization:**
    
    - Terraform initializes a state file after running `terraform apply` for the first time.
2. **Refresh:**
    
    - The `terraform refresh` command updates the state file by querying the current infrastructure.
3. **Locking:**
    
    - To prevent conflicts, Terraform locks the state file during operations in a shared backend.
4. **State Manipulation:**
    
    - **Manual Operations:**
        - Commands like `terraform state mv`, `terraform state rm`, and `terraform state list` allow users to modify or inspect the state.
    - **Importing Resources:**
        - Use `terraform import` to add existing resources into the Terraform state.
5. **Remote State Management:**
    
    - Configure remote state storage to enable collaboration:
## Providers
In Terraform, a **provider** is a plugin that acts as a bridge between Terraform and an external API, enabling Terraform to manage resources for a specific service or platform. Providers are a core component of Terraform, as they define the infrastructure and services that Terraform can interact with.

### Key Concepts of Providers in Terraform

1. **Purpose:**
    
    - Providers enable Terraform to interact with specific APIs, such as those of cloud providers (e.g., AWS, Azure, GCP), SaaS platforms (e.g., GitHub, Datadog), or custom APIs.
    - They handle authentication and API requests to create, read, update, or delete resources.

1. **Examples of Providers:**
    
    - **Cloud Providers:** AWS, Azure, Google Cloud
    - **Infrastructure Tools:** Kubernetes, Helm, Docker
    - **SaaS Applications:** GitHub, PagerDuty, Datadog
    - **Custom APIs:** Custom-built providers for private APIs

1. **Provider Block:**
    
    - The `provider` block in a Terraform configuration specifies which provider to use and configures it with necessary parameters like credentials, regions, or endpoints.
Example:
```hcl
provider "aws" {
  region  = "us-east-1"
  profile = "default"
}
```

6. **Authentication:**
    
    - Providers require authentication credentials to interact with APIs securely.
    - For example, the AWS provider can use credentials from environment variables, a shared credentials file, or an IAM role.
7. **Provider Plugins:**
    
    - Providers are installed as plugins during the `terraform init` phase.
    - They are downloaded from the Terraform Registry or other specified sources.

### How Providers Work

- **Resource and Data Blocks:**  
    Providers expose resources and data sources that Terraform uses to define and manage infrastructure.
    - **Resource Block:** Describes a resource to be created or managed.
    - **Data Block:** Fetches information about existing resources.



## Modules
In Terraform, a **module** is a container(directory) for related configuration files that can be used to organize and reuse infrastructure code. It is a fundamental unit of organization and abstraction, helping users manage complex configurations by breaking them into smaller, manageable components.

### Key Features of a Terraform Module

1. **Organization:**
        - Modules help you logically organize your infrastructure code by grouping related resources together.
2. **Reusability:**
        - Modules can be reused across different projects or environments (e.g., development, staging, production) to avoid code duplication.
3. **Abstraction:**
        - Modules abstract away implementation details, allowing users to interact with a simple interface (input variables and outputs).
### Types of Modules
Terraform has two main types of modules:

1. **Root Module:**
    
    - The directory where Terraform commands like `terraform init`, `terraform plan`, and `terraform apply`are executed is the **root module**.
    - It typically contains the primary configuration files (`.tf` files) and can call child modules.
2. **Child Modules:**
    
    - Modules called from the root module or other modules are referred to as child modules.
    - They are stored in a separate directory and can be sourced from:
        - Local paths (e.g., `./modules/network`)
        - Version-controlled repositories (e.g., GitHub)
        - Terraform Registry (e.g., `terraform-aws-modules/vpc/aws`)

### Structure of a Module
A typical module directory contains:

1. **`main.tf`:** The primary Terraform configuration file defining resources.
2. **`variables.tf`:** Input variables for the module.
3. **`outputs.tf`:** Output values from the module.
4. **`providers.tf`:** (Optional) Provider configurations specific to the module.
5. **`README.md`:** (Optional) Documentation about the module and its usage.

### Using a Module

To use a module, you define it in the `module` block within your configuration, specifying:

- **Source:** Location of the module (local directory, Git repo, Terraform Registry, etc.).
- **Inputs:** Values passed to the module's variables.

Example
```HCL
module "my_vpc" {
  source = "terraform-aws-modules/vpc/aws"
  version = "3.0.0"

  name = "my-vpc"
  cidr = "10.0.0.0/16"

  azs             = ["us-east-1a", "us-east-1b"]
  public_subnets  = ["10.0.1.0/24", "10.0.2.0/24"]
  private_subnets = ["10.0.3.0/24", "10.0.4.0/24"]

  enable_nat_gateway = true
}
```

### Benefits of Using Modules

1. **Simplified Configuration:**
        - Modules encapsulate complexity, making configurations simpler for others to use.
2. **Code Reuse:**
        - Instead of writing the same code repeatedly, you can use a module in multiple places.
3. **Consistency:**
        - Modules enforce consistent resource definitions across environments.
4. **Maintainability:**
        - Updates to a module automatically propagate to all places where it is used (if desired).
