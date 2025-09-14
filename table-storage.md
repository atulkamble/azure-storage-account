Here’s a **quick reference of Azure Table Storage commands** across **Azure CLI**, **PowerShell**, and **.NET SDK / Storage Explorer** for CRUD operations and management:

---

## ⚡ Azure CLI (with `az storage entity` and `az storage table`)

First, set environment variables for convenience:

```bash
export AZURE_STORAGE_ACCOUNT=<your_storage_account>
export AZURE_STORAGE_KEY=<your_access_key>
```

### 1. Create a Table

```bash
az storage table create \
  --name myTable \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

### 2. Insert an Entity (Row)

```bash
az storage entity insert \
  --table-name myTable \
  --entity PartitionKey=demo RowKey=1 Name=Atul Age=30 \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

### 3. Query Entities

```bash
az storage entity query \
  --table-name myTable \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

### 4. Delete an Entity

```bash
az storage entity delete \
  --table-name myTable \
  --partition-key demo \
  --row-key 1 \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

### 5. Delete a Table

```bash
az storage table delete \
  --name myTable \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

## ⚡ PowerShell

Make sure you have **Az.Storage** module installed.

### 1. Create Table

```powershell
$ctx = New-AzStorageContext -StorageAccountName "mystorage" -StorageAccountKey "<key>"
New-AzStorageTable -Name "myTable" -Context $ctx
```

### 2. Insert Entity

```powershell
Add-AzTableRow `
  -Table "myTable" `
  -PartitionKey "demo" `
  -RowKey "1" `
  -Property @{ Name = "Atul"; Age = 30 } `
  -Context $ctx
```

### 3. Query Entities

```powershell
Get-AzTableRow -Table "myTable" -PartitionKey "demo" -Context $ctx
```

### 4. Delete Entity

```powershell
Remove-AzTableRow -Table "myTable" -PartitionKey "demo" -RowKey "1" -Context $ctx
```

### 5. Delete Table

```powershell
Remove-AzStorageTable -Name "myTable" -Context $ctx
```

---

## ⚡ .NET SDK (C# Example)

Install NuGet package:

```bash
dotnet add package Azure.Data.Tables
```

```csharp
using Azure.Data.Tables;

var serviceClient = new TableServiceClient("<connection_string>");
var tableClient = serviceClient.GetTableClient("myTable");
await tableClient.CreateIfNotExistsAsync();

// Insert entity
var entity = new TableEntity("demo", "1")
{
    { "Name", "Atul" },
    { "Age", 30 }
};
await tableClient.AddEntityAsync(entity);

// Query entity
var results = tableClient.Query<TableEntity>(e => e.PartitionKey == "demo");

// Delete entity
await tableClient.DeleteEntityAsync("demo", "1");

// Delete table
await tableClient.DeleteAsync();
```

---

## ⚡ Storage Explorer (GUI Option)

* Open **Azure Storage Explorer** (free desktop tool).
* Connect to your **storage account**.
* Navigate to **Tables → myTable**.
* Right-click → Insert, Query, Delete entities.

---

✅ These commands cover **full CRUD operations** (Create, Read, Update, Delete) for Azure Table Storage in multiple environments.

Would you like me to also prepare a **step-by-step mini-project** (like “Employee Table with CRUD using Azure CLI + PowerShell + SDK”) so you can use it in **Cloudnautic training repos**?
