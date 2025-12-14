## 🔹 Azure Queue Storage – Tutorial

![Image](https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/images/web-queue-worker-physical.png?utm_source=chatgpt.com)

![Image](https://cdn.educba.com/academy/wp-content/uploads/2020/07/Azure-Queue-Storage-architecture.png?utm_source=chatgpt.com)

![Image](https://andrewlock.net/content/images/2024/azure_storage_queue_banner.webp?utm_source=chatgpt.com)

### 📌 What is Azure Queue Storage?

Azure Queue Storage is a **message queuing service** used for **asynchronous communication** between application components.

➡️ It helps **decouple** services so that producers and consumers don’t need to run at the same time.

---

### ✅ Key Use Cases

* Background job processing
* Order processing systems
* Message buffering between microservices
* Traffic smoothing (load leveling)

---

### 🧱 Core Components

| Component          | Description                             |
| ------------------ | --------------------------------------- |
| Storage Account    | Parent container                        |
| Queue              | Holds messages                          |
| Message            | Up to **64 KB**                         |
| Visibility Timeout | Time message stays invisible after read |

---

### 🔧 Create Queue (Azure Portal)

1. Azure Portal → **Storage Accounts**
2. Select Storage Account
3. **Data storage → Queues**
4. Click **+ Queue**
5. Enter name → Create

---

### 🧪 Azure CLI – Queue Creation

```bash
az storage queue create \
  --name myqueue \
  --account-name mystorageaccount
```

---

### 📨 Send Message to Queue

```bash
az storage message put \
  --queue-name myqueue \
  --content "Hello Azure Queue" \
  --account-name mystorageaccount
```

---

### 📥 Read Message from Queue

```bash
az storage message get \
  --queue-name myqueue \
  --account-name mystorageaccount
```

---

### ❌ Delete Message (after processing)

```bash
az storage message delete \
  --queue-name myqueue \
  --id <message-id> \
  --pop-receipt <pop-receipt> \
  --account-name mystorageaccount
```

---

### ⚠️ Important Queue Concepts

* **At-least-once delivery**
* Messages expire after **7 days** (default)
* FIFO *not guaranteed*
* Message invisible while being processed

---

## 🔹 Azure Table Storage – Tutorial

![Image](https://i.ytimg.com/vi/ddhOU0l01-w/sddefault.jpg?utm_source=chatgpt.com)

![Image](https://learn.microsoft.com/en-us/azure/storage/tables/media/storage-table-design-guide/storage-table-design-image12.png?utm_source=chatgpt.com)

![Image](https://learn.microsoft.com/en-us/azure/includes/media/storage-table-concepts-include/table1.png?utm_source=chatgpt.com)

### 📌 What is Azure Table Storage?

Azure Table Storage is a **NoSQL key-value store** for **large amounts of structured data**.

➡️ Ideal for **fast lookups** using keys.

---

### ✅ Key Use Cases

* User profiles
* Application logs
* IoT metadata
* Configuration data

---

### 🧱 Core Concepts

| Concept      | Description                |
| ------------ | -------------------------- |
| Table        | Collection of entities     |
| Entity       | Similar to a row           |
| Properties   | Similar to columns         |
| PartitionKey | Groups entities            |
| RowKey       | Unique ID within partition |

🔑 **PartitionKey + RowKey = Primary Key**

---

### 🔧 Create Table (Azure Portal)

1. Storage Account → **Tables**
2. Click **+ Table**
3. Enter name → Create

---

### 🧪 Azure CLI – Create Table

```bash
az storage table create \
  --name mytable \
  --account-name mystorageaccount
```

---

### ➕ Insert Entity

```bash
az storage entity insert \
  --table-name mytable \
  --entity PartitionKey=Users RowKey=1 Name=Atul Role=Trainer \
  --account-name mystorageaccount
```

---

### 🔍 Query Entities

```bash
az storage entity query \
  --table-name mytable \
  --filter "PartitionKey eq 'Users'" \
  --account-name mystorageaccount
```

---

### ✏️ Update Entity

```bash
az storage entity merge \
  --table-name mytable \
  --entity PartitionKey=Users RowKey=1 City=Pune \
  --account-name mystorageaccount
```

---

### ❌ Delete Entity

```bash
az storage entity delete \
  --table-name mytable \
  --partition-key Users \
  --row-key 1 \
  --account-name mystorageaccount
```

---

### ⚠️ Important Table Concepts

* Schema-less (properties vary per entity)
* Fast reads with proper **PartitionKey design**
* No joins, no foreign keys
* Scales to billions of entities

---

## 🔄 Azure Queue vs Azure Table (Interview Favorite)

| Feature   | Azure Queue      | Azure Table    |
| --------- | ---------------- | -------------- |
| Purpose   | Messaging        | Data storage   |
| Data Type | Messages         | Key-Value      |
| Ordering  | Not guaranteed   | Not applicable |
| Max Size  | 64 KB/message    | 1 MB/entity    |
| Use Case  | Async processing | Fast lookup    |

---

## 🎯 Exam Tips (AZ-900 / AZ-104 / AZ-204)

* **Event notification → Queue**
* **User profile / metadata → Table**
* **Async workload → Queue**
* **NoSQL key-value → Table**

---
