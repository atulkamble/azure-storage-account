# 📦 Azure Storage Accounts: Full Setup with Codes

---

## 📖 Overview

Azure Storage Account is a cloud storage solution providing object, file, queue, table, and disk storage.

---

## 🛠️ Steps to Create a Storage Account

1. **Create a Resource Group**
2. **Create a Storage Account**
3. **Configure Storage Account Options** (like redundancy, access tier, networking)
4. **List, Update, Delete Storage Accounts**

---

## 📌 Azure Storage Services - Key Points

### 🔹 Overview

* Scalable, durable, highly available cloud storage.
* Storage Types: **Blob**, **File Shares**, **Queues**, **Tables**, **Managed Disks**.

### 🔹 Types of Azure Storage

1. **Blob Storage** – Object storage for unstructured data.
2. **File Shares** – Managed file shares accessible via SMB/NFS.
3. **Queue Storage** – Message queueing.
4. **Table Storage** – NoSQL key-value database.
5. **Azure Managed Disks** – Virtual disks for VMs.

### 🔹 Blob Types

* **Block Blob** – For large files.
* **Page Blob** – Random read/write (used for Azure VMs).
* **Append Blob** – Optimized for append operations.

### 🔹 Disk Types

* **Premium SSD (v2/v1)**
* **Standard SSD**
* **Standard HDD**

### 🔹 Access Keys & SAS

* **Access Keys**: Full access to storage account.
* **SAS Token**: Limited, time-restricted access.

### 🔹 Data Protection & Redundancy

* **Replication Types**: LRS, ZRS, GRS, GZRS, RAGRS, RAGZRS
* **Features**: Versioning, Soft Delete, Snapshot, Change Feed, Object Replication, Inventory, Lifecycle Policies.

### 🔹 Static Website Hosting & CDN

* Host static web apps via Storage Account.
* Integrate with Azure CDN for global delivery.

---

## 🕌 Azure CLI Commands

> Ensure you're logged in:

```bash
az login
```

**Create Resource Group**

```bash
az group create --name MyResourceGroup --location eastus
```

**Create Storage Account**

```bash
az storage account create \
  --name mystorageacct12345 \
  --resource-group MyResourceGroup \
  --location eastus \
  --sku Standard_LRS \
  --kind StorageV2 \
  --access-tier Hot
```

**List Storage Accounts**

```bash
az storage account list --resource-group MyResourceGroup -o table
```

**Show Storage Account Details**

```bash
az storage account show --name mystorageacct12345 --resource-group MyResourceGroup
```

**Delete Storage Account**

```bash
az storage account delete --name mystorageacct12345 --resource-group MyResourceGroup
```

**List Storage Account Keys**

```bash
az storage account keys list --account-name mystorageacct12345 --resource-group MyResourceGroup -o table
```

---

## 🕌 Azure PowerShell Commands

> Ensure you're logged in:

```powershell
Connect-AzAccount
```

**Create Resource Group**

```powershell
New-AzResourceGroup -Name MyResourceGroup -Location "East US"
```

**Create Storage Account**

```powershell
New-AzStorageAccount -ResourceGroupName "MyResourceGroup" `
  -Name "mystorageacct12345" `
  -Location "East US" `
  -SkuName "Standard_LRS" `
  -Kind "StorageV2" `
  -AccessTier "Hot"
```

**List Storage Accounts**

```powershell
Get-AzStorageAccount -ResourceGroupName "MyResourceGroup"
```

**Delete Storage Account**

```powershell
Remove-AzStorageAccount -ResourceGroupName "MyResourceGroup" -Name "mystorageacct12345"
```

---

## 🕌 ARM Template

📄 `storageAccount.json`

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountName": {
      "type": "string"
    },
    "location": {
      "type": "string",
      "defaultValue": "eastus"
    }
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2023-01-01",
      "name": "[parameters('storageAccountName')]",
      "location": "[parameters('location')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "StorageV2",
      "properties": {
        "accessTier": "Hot"
      }
    }
  ]
}
```

**Deploy ARM Template**

```bash
az deployment group create --resource-group MyResourceGroup --template-file storageAccount.json --parameters storageAccountName=mystorageacct12345
```

---

## 🕌 Bicep Template

📄 `storageAccount.bicep`

```bicep
param storageAccountName string
param location string = 'eastus'

resource storageAccount 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: storageAccountName
  location: location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
  properties: {
    accessTier: 'Hot'
  }
}
```

**Deploy Bicep Template**

```bash
az deployment group create --resource-group MyResourceGroup --template-file storageAccount.bicep --parameters storageAccountName=mystorageacct12345
```

---

## 🕌 Terraform

📄 `main.tf`

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "example" {
  name     = "MyResourceGroup"
  location = "East US"
}

resource "azurerm_storage_account" "example" {
  name                     = "mystorageacct12345"
  resource_group_name      = azurerm_resource_group.example.name
  location                 = azurerm_resource_group.example.location
  account_tier             = "Standard"
  account_replication_type = "LRS"
  account_kind             = "StorageV2"
  access_tier              = "Hot"
}
```

**Deploy Terraform Configuration**

```bash
terraform init
terraform plan
terraform apply
```

---

## 🕌 Repo Suggestion Name

👉 `azure-storage-account-provisioning`

**Structure:**

```
azure-storage-account-provisioning/
├── cli/
│   └── storage-account-cli.sh
├── powershell/
│   └── storage-account.ps1
├── arm-template/
│   └── storageAccount.json
├── bicep/
│   └── storageAccount.bicep
├── terraform/
│   ├── main.tf
│   └── variables.tf
└── README.md
```

---

## 📚 Summary

* ✅ Azure CLI
* ✅ Azure PowerShell
* ✅ ARM Template
* ✅ Bicep
* ✅ Terraform
