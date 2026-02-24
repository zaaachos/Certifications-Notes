# Microsoft Certified: Azure Administrator Associate (AZ-104)

Configure and manage Azure services and resources. Manage virtual networks, storage, compute, and Azure identities.

- ### Microsoft Learn [link](https://learn.microsoft.com/en-us/credentials/certifications/azure-administrator/)

## [AZ-104: Prerequisites for Azure administrators](https://learn.microsoft.com/en-us/training/paths/az-104-administrator-prerequisites/)

- ### [Introduction to Azure Cloud Shell](https://learn.microsoft.com/en-us/training/modules/intro-to-azure-cloud-shell/)
  - **Azure Cloud Shell**
    - Cloud-based shell environment accessible from the Azure portal
    - Provides integrated command-line interface for managing Azure resources
    - No local installation required

  - **Learning objectives**
    - Describe Azure Cloud Shell and the functionality it provides
    - Determine whether Azure Cloud Shell meets the needs of your organization
    - Recognize how to use Azure Cloud Shell and persist files for multiple sessions

  - **Key Concepts**
    - **Accessing Cloud Shell**
      - Direct link: https://shell.azure.com
      - From Azure portal
      - From code snippets on Microsoft Learn

    - **Cloud Shell Session**
      - Temporary host (VM) allocated to each session
      - Preconfigured with latest versions of PowerShell and Bash
      - User selects preferred shell experience (Bash or PowerShell)
      - Sessions terminate after 20 minutes of inactivity
      - Files on CloudDrive are persisted after session termination

    - **File Management**
      - **CloudDrive**: Persist files across sessions
      - **Azure File Share Mapping**: Access shared storage tied to specific regions
      - **Cloud Shell Editor**: Edit files using curly brackets {} icon or `code` command (Classic mode)

    - **Preinstalled Tools**
      - **Linux tools**: bash, zsh, sh, tmux, dig
      - **Azure tools**: Azure CLI, AzCopy, Azure Functions CLI, Service Fabric CLI, Batch Shipyard, blobxfer
      - **Text editors**: code (Cloud Shell editor), vim, nano, emacs
      - **Source control**: git
      - **Build tools**: make, maven, npm, pip
      - **Containers**: Docker, Machine, Kubectl, Helm, DC/OS CLI
      - **Databases**: MySQL client, PostgreSQL client, sqlcmd, mssql-scripter
      - **Other**: Terraform, Ansible, Chef, InSpec, Puppet, Bolt, Packer, Office 365 CLI

- ### [Deploy Azure infrastructure by using JSON ARM templates](https://learn.microsoft.com/en-us/training/modules/create-azure-resource-manager-template-vs-code/)
  - **Azure Resource Manager (ARM) Templates**
    - Infrastructure-as-Code (IaC) approach using JSON format
    - Deploy resources consistently and reliably to Azure
    - Declarative approach to infrastructure provisioning

  - **Learning objectives**
    - Implement a JSON ARM template by using Visual Studio Code
    - Declare resources and add flexibility to your template by adding resources, parameters, and outputs

  - **Infrastructure as Code (IaC)** - Describe infrastructure through code so deployments are consistent, auditable and versionable. - ARM templates are idempotent: repeated deployments produce the same state.
  - **File sections (common)**
    - `$schema`: JSON schema location for the template (required).
    - `contentVersion`: Template version (required) — use to track significant changes.
    - `apiProfile`: Optional collection of API versions to avoid per-resource apiVersion entries.
    - `parameters`: Optional — values provided at deployment time (files, CLI, portal).
    - `variables`: Optional — reusable values to simplify expressions.
    - `functions`: Optional — user-defined functions for repeated complex expressions.
    - `resources`: Required — resource declarations to create/update (type, apiVersion, name, location, properties).
    - `outputs`: Optional — values returned after deployment completes.

  - **Declarative model**
    - Describe desired resources and properties; Azure Resource Manager handles ordering, parallelism and validation.

  - **Adding resources**
    - Resource `type` is `{resource-provider}/{resource-type}` (e.g. `Microsoft.Storage/storageAccounts`).
    - Check the Azure templates/docs for available properties and supported `apiVersion` for each resource type.
    - Common resource fields: `type`, `apiVersion`, `name`, `location`, `sku`, `kind`, `properties`.

  - **Deploying templates**
    - Deployment options: local template, linked templates, or CI/CD pipelines (Azure Pipelines / GitHub Actions).
    - Use Azure CLI / PowerShell. Example steps with Azure CLI:

    ```bash
    az login
    az group create --name myResourceGroup --location westus
    templateFile="{path-to-template}"
    az deployment group create --name myDeployment --resource-group myResourceGroup --template-file $templateFile
    ```

    - Prefer `az deployment group create` (newer command) over deprecated `az group deployment create`.

- **Parameters & Outputs (Add flexibility)**
  - **Parameters**
    - Let you provide values at deployment time (CLI, portal, or parameter file).
    - Common parameter properties: `type`, `defaultValue`, `allowedValues`, `minLength`, `maxLength`, `minValue`, `maxValue`, `metadata`, `secureValue`/`secureString`.
    - Parameter `types`: `string`, `int`, `bool`, `array`, `object`, `secureString`, `secureObject`.
    - Use `allowedValues` to restrict choices; use `defaultValue` for sensible defaults.
    - Use `secureString` / `secureObject` for secrets (values are masked in portal/outputs).
    - Parameter files: JSON files that supply parameter values for repeatable deployments.

  - **Parameters - example**

  ```json
  "parameters": {
  "storageAccountName": {
      "type": "string",
      "defaultValue": "learnstorage",
      "metadata": { "description": "Name for the storage account" }
  },
  "skuName": {
      "type": "string",
      "allowedValues": ["Standard_LRS","Standard_GRS"],
      "defaultValue": "Standard_LRS"
  }
  }
  ```

  - **Outputs**
 ` - Return values from the deployment (resource IDs, connection strings, names) visible in portal/CLI after deployment.
  - Useful for chaining deployments, passing values to linked templates, or CI/CD tasks.`

  - **Outputs - example**

  ```json
  "outputs": {
  "storageAccountId": {
      "type": "string",
      "value": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]"
  }
  }
  ```

  - **Passing parameters via Azure CLI**
    - Single param: `--parameters storageAccountName=myname skuName=Standard_LRS`
    - Parameter file: `--parameters @params.json` where `params.json` contains the `parameters` object.

  - **Notes / Tips**
    - Avoid exposing secrets in `outputs` — use Key Vault for sensitive values.
    - Use variables/functions to centralize common expressions and reduce repetition.
    - Validate templates locally with `az deployment group validate` before creating deployments.

  - **Complex deployments**
    - Break complex solutions into smaller, reusable templates and link them (linked or nested templates).
    - Store linked templates securely (e.g., with SAS tokens) and orchestrate from a main template or CI/CD.

  - **Example snippet (storage account)**
    - Minimal example fields you will commonly use in a `resources` array (apiVersion, name, location, sku, kind, properties).
    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.1",
      "apiProfile": "",
      "parameters": {},
      "variables": {},
      "functions": [],
      "resources": [
        {
          "type": "Microsoft.Storage/storageAccounts",
          "apiVersion": "2025-01-01",
          "name": "learntemplatestorage123",
          "location": "westus",
          "sku": {
            "name": "Standard_LRS"
          },
          "kind": "StorageV2",
          "properties": {
            "supportsHttpsTrafficOnly": true
          }
        }
      ],
      "outputs": {}
    }
    ```
