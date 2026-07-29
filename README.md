# Terraform-Azure-Enterprise-Landing-Zone
Design, provision, and manage a secure, modular Azure cloud environment using Terraform. This project will serve as a foundational "landing zone" demonstrating modern Infrastructure as Code (IaC) principles, network segmentation, and security governance.

### Real-World Business Scenario:
Globex Corporation, a mid-sized enterprise, is migrating its legacy on-premises infrastructure to Microsoft Azure. To avoid the configuration drift and security vulnerabilities that plagued their on-prem environment, leadership has mandated that all new cloud infrastructure must be deployed via code.

They need a standardized, secure network backbone that logically separates their core departments—IT, Engineering, Finance, Marketing, and Human Resources—while centralizing security logging, secrets management, and access controls.

### Core Technologies & Concepts
Azure Services: Resource Groups, Virtual Networks (VNets), Subnets, Network Security Groups (NSGs), Storage Accounts, Azure Key Vault, Virtual Machines (B-series for cost efficiency), and Log Analytics Workspaces.

Terraform Concepts: Providers, Resource blocks, Variables (.tfvars), Outputs, Local values, Remote State (Backend), State Locking, Modules, for_each and count meta-arguments, and Data Sources.

Skills Gained: Infrastructure as Code lifecycle, declarative cloud provisioning, cloud network isolation, secrets management, security governance via code, and professional Git repository management.

### Project Roadmap
We will build this incrementally. Each stage will introduce new concepts while building upon the last, keeping costs as close to zero as possible.

- Stage 1: Foundational Setup & Remote State. Configuring the Azure provider, setting up the repository, and provisioning a secure Azure Storage Account to act as our remote Terraform backend.

- Stage 2: The Network Backbone. Building the VNet and programmatically looping through our business departments (IT, Engineering, Finance, HR, Marketing) to create isolated subnets using Terraform collections (for_each).

- Stage 3: Security & Governance. Implementing Network Security Groups (NSGs) to restrict traffic between departments and enforcing enterprise resource tagging standards.

- Stage 4: Secrets & Observability. Provisioning an Azure Key Vault for secure secrets management and a Log Analytics Workspace to centralize infrastructure logging.
  
- Stage 5: Modularization & Refactoring. Taking the monolithic code we've written and breaking it down into reusable modules, reflecting senior-level engineering practices.
  
- Stage 6: Compute & Validation. Deploying a low-cost Virtual Machine to validate network routing and security rules, followed by infrastructure teardown and documentation finalization.

## Stage 1: Foundational Setup & Remote State
Objectives
- Initialize the local repository with professional directory structuring.
- Authenticate with Azure using the Azure CLI.
- Bootstrap an Azure Storage Account and Blob Container to host the Terraform state file.
- Configure the Terraform backend to use the newly created remote storage.

### Business Justification
By default, Terraform stores its state locally in a terraform.tfstate file. In an enterprise environment, this is a catastrophic security and operational risk. Local state files cannot be shared among team members, leading to configuration conflicts. More importantly, state files store infrastructure secrets (like database passwords and API keys) in plain text. Migrating to a remote backend with encryption, RBAC controls, and versioning is a mandatory first step for any production-grade deployment.

Azure Services Used
- Resource Group: Logical container for the backend infrastructure.
- Storage Account: Globally unique, secure storage resource.
- Blob Container: Specific repository for the state file.

Terraform Concepts Introduced
- The terraform block: Defining required versions and the backend configuration.
- The provider block: Instructing Terraform to interact with the Azure Resource Manager (azurerm) API.
- terraform init: The command that downloads provider plugins and initializes the backend connection.
