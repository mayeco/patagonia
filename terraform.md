---
description: Scan projects and generate Terraform infrastructure as code automatically
---

# Terraform Infrastructure Detection Workflow

Scan the current project and automatically detect infrastructure requirements through dependencies, environment variables, configuration files, and other indicators. Generate a complete /terraform folder with appropriate Terraform files for deploying the project.

## Steps

0. Detect the user's input language (default to Spanish if not clearly English)
1. If no clear English indicators are found, default to Spanish for all responses
2. Scan project structure and files:
   - Analyze package.json, requirements.txt, pom.xml, go.mod for dependencies
   - Check for environment variables in .env files, docker-compose.yml
   - Identify framework and runtime (Node.js, Python, Java, Go, etc.)
   - Detect database usage from ORM configurations, connection strings
   - Check for cloud service integrations (AWS SDK, Google Cloud client libraries)
   - Analyze Docker files for containerization requirements
   - Review CI/CD files for deployment patterns

3. Detect infrastructure components needed:
   - **Compute Resources**: EC2 instances, Lambda functions, App Engine, Cloud Run
   - **Storage**: S3 buckets, Cloud Storage, databases (RDS, Cloud SQL)
   - **Networking**: VPC, subnets, security groups, load balancers
   - **Security**: IAM roles, service accounts, API keys management
   - **Monitoring**: CloudWatch, Cloud Monitoring, logging
   - **CDN**: CloudFront, Cloud CDN for static assets

4. Determine cloud provider preferences:
   - Check for existing cloud configurations (AWS credentials, GCP service accounts)
   - Analyze SDK imports and API calls
   - Consider cost optimization and regional preferences
   - **DEFAULT TO GOOGLE CLOUD** if no specific provider is detected or specified

5. Generate Terraform configuration:
   - Create main.tf with detected resources
   - Generate variables.tf for configurable parameters
   - Create outputs.tf for resource references
   - Generate terraform.tfvars with detected values
   - Create provider.tf with appropriate cloud provider configuration

6. Create supporting files:
   - Generate .terraformignore file
   - Create README.md with deployment instructions
   - Generate scripts for common operations (plan, apply, destroy)
   - Create .env.example for environment variables

7. Validate generated configuration:
   - Run terraform validate to check syntax
   - Verify resource dependencies and references
   - Check for security best practices
   - Validate variable definitions and defaults

8. Generate deployment documentation:
   - Create step-by-step deployment guide
   - Document required permissions and prerequisites
   - Include cost estimation commands
   - Provide rollback procedures

9. Create infrastructure modules:
   - Generate reusable modules for common patterns
   - Create environment-specific configurations
   - Include monitoring and alerting setup
   - Add backup and disaster recovery configurations

## Infrastructure Detection Methods

### Dependency Analysis

#### Node.js Projects
```bash
# Check package.json for cloud dependencies
cat package.json | jq '.dependencies | keys[] | select(contains("aws") or contains("gcp") or contains("azure"))'

# Detect framework from dependencies
# Express.js → API Gateway + Lambda
# Next.js → Static hosting + API routes
# NestJS → ECS or App Runner
```

#### Python Projects
```bash
# Check requirements.txt for cloud SDKs
grep -E "(boto3|google-cloud|azure)" requirements.txt

# Django → RDS + Elastic Beanstalk or ECS
# Flask → API Gateway + Lambda
# FastAPI → API Gateway + Lambda with API documentation
```

#### Java Projects
```bash
# Check pom.xml or build.gradle for AWS SDK
grep -E "(aws-sdk|spring-cloud)" pom.xml

# Spring Boot → ECS or Elastic Beanstalk
# Micronaut → Lambda with custom runtime
# Quarkus → Lambda with GraalVM native image
```

### Environment Detection

#### Database Detection
```bash
# Check for database connection strings
grep -r "DATABASE_URL\|DB_CONNECTION\|MONGO_URI" .

# PostgreSQL → RDS instance
# MongoDB → DocumentDB or Atlas
# Redis → ElastiCache
# MySQL → RDS MySQL
```

#### Storage Detection
```bash
# Check for file upload or storage usage
grep -r "multer\|boto3.*s3\|cloud-storage" .

# File uploads → S3 bucket
# Static assets → CloudFront + S3
# User uploads → S3 with CDN
```

#### External Services
```bash
# Check for external API integrations
grep -r "STRIPE\|SENDGRID\|TWILIO\|SLACK" .

# Payment processing → API Gateway + Lambda
# Email service → SES or SendGrid
# Notifications → SNS or webhooks
```

## Generated Terraform Structure

### Basic Project Structure
```
terraform/
├── main.tf           # Main infrastructure resources
├── variables.tf      # Input variables
├── outputs.tf        # Output values
├── terraform.tfvars  # Variable values
├── provider.tf       # Cloud provider configuration
├── .terraformignore  # Files to ignore
├── README.md         # Deployment documentation
└── scripts/
    ├── plan.sh       # Terraform plan script
    ├── apply.sh      # Terraform apply script
    └── destroy.sh    # Terraform destroy script
```

### Advanced Structure with Modules
```
terraform/
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
├── provider.tf
├── modules/
│   ├── compute/      # EC2, Lambda, etc.
│   ├── storage/      # S3, databases, etc.
│   ├── networking/   # VPC, subnets, etc.
│   └── monitoring/   # CloudWatch, alerts, etc.
├── environments/
│   ├── dev/
│   ├── staging/
│   └── prod/
└── scripts/
    ├── deploy.sh
    └── cleanup.sh
```

## Cloud Provider Templates

### AWS Template
```hcl
# provider.tf
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

provider "aws" {
  region = var.region
}

# main.tf
resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = var.instance_type

  tags = {
    Name = "${var.project_name}-web"
  }
}

# variables.tf
variable "region" {
  description = "AWS region"
  type        = string
  default     = "us-east-1"
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t3.micro"
}
```

### GCP Template
```hcl
# provider.tf
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "~> 4.0"
    }
  }
}

provider "google" {
  project = var.project_id
  region  = var.region
}

# main.tf
resource "google_compute_instance" "web" {
  name         = "${var.project_name}-web"
  machine_type = var.machine_type
  zone         = var.zone

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-11"
    }
  }

  network_interface {
    network = "default"
    access_config {}
  }
}
```

### Azure Template
```hcl
# provider.tf
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0"
    }
  }
}

provider "azurerm" {
  features {}
}

# main.tf
resource "azurerm_resource_group" "main" {
  name     = "${var.project_name}-rg"
  location = var.location
}

resource "azurerm_linux_virtual_machine" "web" {
  name                = "${var.project_name}-web"
  resource_group_name = azurerm_resource_group.main.name
  location            = azurerm_resource_group.main.location
  size                = var.vm_size
  admin_username      = var.admin_username

  network_interface_ids = [
    azurerm_network_interface.main.id,
  ]

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }
}
```

## Common Infrastructure Patterns

### Web Application
- **Frontend**: S3 + CloudFront or Cloud Storage + CDN
- **Backend**: Lambda/API Gateway or ECS/App Runner
- **Database**: RDS or Cloud SQL
- **Cache**: ElastiCache or Memorystore

### Microservices
- **Service Discovery**: ECS Service Discovery or Cloud Map
- **API Gateway**: API Gateway or Cloud Endpoints
- **Load Balancing**: ALB or Load Balancer
- **Monitoring**: CloudWatch or Cloud Monitoring

### Data Processing
- **Compute**: EMR or Dataproc for big data
- **Storage**: S3 or Cloud Storage for data lake
- **Databases**: Redshift or BigQuery for analytics
- **Orchestration**: Step Functions or Cloud Composer

## Deployment Scripts

### Plan and Apply
```bash
#!/bin/bash
# scripts/plan.sh
cd "$(dirname "$0")/.."

echo "Initializing Terraform..."
terraform init

echo "Planning infrastructure changes..."
terraform plan -var-file="terraform.tfvars" -out=tfplan

echo "Review the plan above and run 'terraform apply tfplan' to apply changes."
```

### Destroy Infrastructure
```bash
#!/bin/bash
# scripts/destroy.sh
cd "$(dirname "$0")/.."

echo "WARNING: This will destroy all infrastructure!"
read -p "Are you sure? (yes/no): " confirm

if [ "$confirm" = "yes" ]; then
    terraform destroy -var-file="terraform.tfvars"
else
    echo "Destroy cancelled."
fi
```

## Cost Estimation

### AWS Cost Commands
```bash
# Estimate monthly costs
terraform plan -var-file="terraform.tfvars" > plan.txt
infracost breakdown --path=plan.txt

# Detailed cost analysis
infracost diff --path=plan.txt
```

### GCP Cost Commands
```bash
# Estimate costs using gcp-price-calculator
terraform show -json > plan.json
# Use GCP pricing calculator with the JSON output
```

## Security Best Practices

### IAM and Permissions
- Use least privilege principle
- Rotate access keys regularly
- Use IAM roles instead of access keys when possible
- Enable multi-factor authentication

### Network Security
- Use VPCs and security groups
- Implement network segmentation
- Use HTTPS everywhere
- Configure firewalls properly

### Data Protection
- Encrypt data at rest and in transit
- Use managed database services
- Implement backup strategies
- Configure monitoring and alerting

## Troubleshooting

### Common Issues
- **Provider authentication**: Check credentials and permissions
- **Resource dependencies**: Ensure resources are created in correct order
- **Variable validation**: Check variable types and defaults
- **State management**: Handle terraform state carefully

### Validation Commands
```bash
# Validate configuration
terraform validate

# Format configuration
terraform fmt

# Check for updates
terraform plan -refresh-only

# Debug issues
TF_LOG=DEBUG terraform apply
```

**IMPORTANT:** Always provide responses in Spanish by default, unless the developer clearly specifies English.

**Language Support:**
- **Spanish**: DEFAULT - Escanear proyecto y generar Terraform en español para TODA entrada
- **English**: Generate Terraform in English only if explicitly requested
- **Other**: Generate Terraform in Spanish as default, but adapt to detected language when possible

**Prerequisites:**
- Terraform CLI installed (version 1.0+)
- Cloud provider credentials configured
- Project files accessible for scanning
- Basic understanding of infrastructure concepts
- Cost management approval for cloud resources