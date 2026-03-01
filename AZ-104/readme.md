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
## [AZ-104: Manage identities and governance in Azure](https://learn.microsoft.com/en-us/training/paths/az-104-manage-identities-governance/)

- ### [Understand Microsoft Entra ID](https://learn.microsoft.com/en-us/training/modules/understand-azure-active-directory/)
  - Cloud-based identity and access management (IAM) service for Azure and Microsoft 365.
  - Manages users, groups, and devices; supports SSO for apps.

  - Directory service for Microsoft cloud apps (Azure, M365, Intune, Dynamics 365).
  - Centralized authentication/authorization for all Microsoft cloud services via a single Entra tenant.
  - Enables SSO for users across Microsoft and external apps (Google, Facebook, etc.).
  - Integrates with other identity providers and on-prem AD DS.

  - Entra ID P1 vs P2 plans:
    - P1: Adds self-service group mgmt, advanced security reports, full MFA, MIM licensing, 99.9% SLA, password reset w/ writeback, Cloud App Discovery, Conditional Access, Connect Health.
    - P2: All P1 features plus Identity Protection (risk-based policies, user risk detection) and Privileged Identity Management (PIM) for just-in-time admin access.
    - Both require extra licensing (standalone or via EMS E3/E5).
    - Always check Microsoft docs for latest plan details.

  - Azure AD Domain Services (AAD DS):
    - Provides managed domain services (domain join, group policy, LDAP, Kerberos/NTLM) without deploying domain controllers.
    - Useful for legacy apps that require traditional AD features but in the cloud.
    - No direct domain admin access; managed by Microsoft.
    - Azure AD vs. AAD DS:
      - Azure AD: Modern IAM, SSO, cloud-first, no domain join or group policy.
      - AAD DS: Adds domain join, legacy protocol support for cloud VMs, but not a replacement for full on-prem AD.

- ### [Create, configure, and manage identities](https://learn.microsoft.com/en-us/training/modules/create-configure-manage-identities/)

  *Create, configure, and manage users*
  - Every user accessing Azure resources needs an Azure user account.
  - User account contains authentication info needed for sign-on.
  - Once authenticated, Microsoft Entra ID builds an access token that determines resource access and permissions.

  *Accessing user management:*
  - Use the Microsoft Entra ID dashboard in Azure portal to manage user objects.
  - Go to Identity > Users > All Users to view all users.
  - User Type column displays members and guests.
  - Can only work with one directory at a time; use Directory + Subscription panel or Switch directory button to change directories.

  *Three types of users in Microsoft Entra ID:*
  - *Cloud identities:* Exist only in Microsoft Entra ID. Examples: admin accounts, self-managed users. Source: Microsoft Entra ID or External Microsoft Entra directory. Deleted when removed from primary directory.
  - *Directory-synchronized identities:* From on-premises Active Directory. Synced to Azure via Microsoft Entra Connect. Source: Windows Server AD.
  - *Guest users:* Exist outside Azure. Examples: other cloud providers, Microsoft accounts (Xbox LIVE). Source: Invited user. Useful for vendors/contractors. Can be removed entirely with all access revoked.

  *Create, configure, and manage groups*
  - Microsoft Entra groups organize users to simplify permission management.
  - Assign permissions to groups instead of individually; add/remove users to grant/deny access.
  - Can define membership based on rules (e.g., department, job title).
  - View all groups via Identity > Groups in Microsoft Entra admin center.

  *Two types of groups:*
  - *Security groups:* Most common. Manage member and computer access to shared resources. Requires Microsoft Entra administrator to create.
  - *Microsoft 365 groups:* Provide collaboration (shared mailbox, calendar, files, SharePoint site). Available to users and admins. Can grant access to external people.

  *Membership types:*
  - *Assigned:* Members added and maintained manually.
  - *Dynamic:* Members added automatically based on rules. Membership updates dynamically as attribute values change.

  *Dynamic groups:*
  - Membership generated by formula each time group is used.
  - Includes recipients with attribute values matching the filter.
  - If a user's properties change to match filter, they automatically become members.
  - Well-defined account provisioning processes reduce accidental membership additions.

  *Configure and manage device registration*
  - Device management balances user productivity (anywhere, any device) with organizational asset protection.
  - Microsoft Entra ID enables device identity management; use Microsoft Intune for security/compliance standards.
  - Microsoft Entra ID provides SSO to devices, apps, and services.

  *Microsoft Entra registered devices (BYOD scenarios):*
  - Users access organizational resources via personal devices using local credentials + Microsoft account.
  - Operating systems: Windows 10/11, iOS, Android, macOS.
  - Device management via MDM (e.g., Microsoft Intune).
  - Key capabilities: SSO to cloud resources, Conditional Access.
  - Scenarios: Home PC accessing organizational email/benefits, personal phone with rooted device blocking.
  - Registration via work application or Windows Settings.

  *Microsoft Entra joined devices (cloud-first/cloud-only):*
  - Devices joined only to Microsoft Entra ID; requires organizational account to sign in.
  - Operating systems: All Windows 10/11 (except Home), no down-level support by default.
  - Device management via MDM (Microsoft Intune) or co-management (Endpoint Configuration Manager).
  - Key capabilities: SSO to cloud/on-premises resources, Conditional Access, Self-service Password Reset, Windows Hello PIN reset.
  - Deployment: Self-service (OOBE), bulk enrollment, Windows Autopilot.
  - Use cases: Cloud-based infrastructure transition, mobile devices (tablets/phones), Microsoft 365/SaaS access, remote workers with limited on-prem infrastructure.

  *Hybrid Microsoft Entra joined devices (on-premises + cloud):*
  - Joined to on-premises AD and registered with Microsoft Entra ID simultaneously.
  - Operating systems: Windows 11, 10, 8.1, 7; Windows Server 2008/R2, 2012/R2, 2016, 2019.
  - Device management via Group Policy, Configuration Manager standalone, or co-management with Intune.
  - Key capabilities: SSO to cloud/on-premises, Conditional Access, Self-service Password Reset, Windows Hello PIN reset.
  - Scenarios: Win32 apps needing AD machine authentication, continuing Group Policy/imaging solutions, supporting legacy Windows 7/8.1 devices.

  *Device writeback:*
  - Keeps track of devices registered with Microsoft Entra ID in on-premises AD.
  - Stores device objects in "Registered Devices" container.
  - Use case: Enable on-premises conditional access (e.g., ADFS claim rules check device status before granting access).
  - Required for Windows Hello for Business (WHFB) in Hybrid and Federated scenarios.

  *Auto provisioning (SCIM)*
  - SCIM 2.0: open standard for automating user/group lifecycle between HCM → Entra → target apps.
  - Core components: HCM (source of truth), Entra Provisioning Service (SCIM connector), Microsoft Entra ID (identity store), Target app (SCIM endpoint).
  - Benefits: automatic provisioning/deprovisioning, faster offboarding, reduced orphaned accounts, consistent attribute sync.
  - Quick checklist: define attribute mappings; set scoping filters; configure secure connector creds (prefer OAuth2); test in a sandbox; enable logging and reconciliation.


- ### [Describe the core architectural components of Azure](https://learn.microsoft.com/en-us/training/modules/describe-core-architectural-components-of-azure/)


- ### [Azure Policy initiatives](https://learn.microsoft.com/en-us/training/modules/sovereignty-policy-initiatives/)


- ### [Secure your Azure resources with Azure role-based access control (Azure RBAC)](https://learn.microsoft.com/en-us/training/modules/secure-azure-resources-with-rbac/)


- ### [Allow users to reset their password with Microsoft Entra self-service password reset](https://learn.microsoft.com/en-us/training/modules/allow-users-reset-their-password/)