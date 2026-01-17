![Image](https://scotthelme.co.uk/content/images/2015/06/table-storage-partitions-diagram.png)

![Image](https://learn.microsoft.com/en-us/azure/storage/tables/media/storage-table-design-guide/storage-table-design-image12.png)

![Image](https://cdn-dynmedia-1.microsoft.com/is/image/microsoftcorp/value-prop?fit=constrain\&fmt=png-alpha\&op_usm=1.5%2C0.65%2C15%2C0\&qlt=100\&resMode=sharp2\&wid=847)

# 🔹 Azure Table Storage – Basic Documentation (Simple & Clear)

## 📌 What is Azure Table Storage?

Azure Table Storage is a **NoSQL key-value storage service** used to store **structured data** at large scale.

* No joins
* No fixed schema
* Fast access using keys

---

## 🧱 Core Concepts (Must Know)

| Term         | Meaning            |
| ------------ | ------------------ |
| Table        | Collection of rows |
| Entity       | Single row         |
| Property     | Column             |
| PartitionKey | Groups data        |
| RowKey       | Unique ID          |

🔑 **PartitionKey + RowKey = Primary Key**

---

## 🧪 Azure CLI – BASIC Commands Only

### 🔐 Set Variables

```bash
export AZURE_STORAGE_ACCOUNT=mystorage
export AZURE_STORAGE_KEY=<key>
```

---

### 1️⃣ Create Table

```bash
az storage table create \
  --name demoTable \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

### 2️⃣ Insert Entity

```bash
az storage entity insert \
  --table-name demoTable \
  --entity PartitionKey=Users RowKey=1 Name=Atul City=Pune \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

### 3️⃣ Read / Query Entity

```bash
az storage entity query \
  --table-name demoTable \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

### 4️⃣ Update Entity

```bash
az storage entity merge \
  --table-name demoTable \
  --entity PartitionKey=Users RowKey=1 City=Mumbai \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

### 5️⃣ Delete Entity

```bash
az storage entity delete \
  --table-name demoTable \
  --partition-key Users \
  --row-key 1 \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

### 6️⃣ Delete Table

```bash
az storage table delete \
  --name demoTable \
  --account-name $AZURE_STORAGE_ACCOUNT \
  --account-key $AZURE_STORAGE_KEY
```

---

## ⚡ PowerShell – BASIC

### Create Context

```powershell
$ctx = New-AzStorageContext `
  -StorageAccountName "mystorage" `
  -StorageAccountKey "<key>"
```

---

### Create Table

```powershell
New-AzStorageTable -Name "demoTable" -Context $ctx
```

---

### Insert Entity

```powershell
Add-AzTableRow `
  -Table "demoTable" `
  -PartitionKey "Users" `
  -RowKey "1" `
  -Property @{ Name="Atul"; City="Pune" } `
  -Context $ctx
```

---

### Read Entity

```powershell
Get-AzTableRow -Table "demoTable" -PartitionKey "Users" -Context $ctx
```

---

### Delete Entity

```powershell
Remove-AzTableRow -Table "demoTable" -PartitionKey "Users" -RowKey "1" -Context $ctx
```

---

## ⚡ .NET SDK (C# – Minimal)

```csharp
using Azure.Data.Tables;

var client = new TableClient("<connection_string>", "demoTable");

// Insert
var entity = new TableEntity("Users", "1");
entity["Name"] = "Atul";
entity["City"] = "Pune";
client.AddEntity(entity);

// Read
var result = client.Query<TableEntity>(e => e.PartitionKey == "Users");

// Delete
client.DeleteEntity("Users", "1");
```

---

## 🖥️ GUI – Azure Storage Explorer

* Open Storage Explorer
* Storage Account → Tables
* Right-click → Insert / Edit / Delete

(No code needed)

---

## ⚠️ Simple Rules (Interview)

* NoSQL = No joins
* Fast lookup = Good PartitionKey
* Entity size max = **1 MB**
* Schema-less storage

---

## 🎯 Exam Tip (AZ-900 / AZ-104)

* **User data → Table Storage**
* **Messages → Queue Storage**
* **Key-Value data → Table**

---

### ✅ This version is:

✔ Beginner friendly
✔ Minimal commands
✔ Classroom ready
✔ Interview oriented
