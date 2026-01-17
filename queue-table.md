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
