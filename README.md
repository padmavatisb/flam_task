
# QueueCTL — Background Job Queue CLI

`queuectl` is a lightweight background job queue system implemented in Python using SQLite.  
It allows you to enqueue tasks, run workers to process them, retry on failure with exponential backoff, and move permanently failed jobs to a **Dead Letter Queue (DLQ)**.

This was built as part of the **Backend Developer Internship Assignment**.

---

## 🚀 Features

| Feature | Description |
|--------|-------------|
| Enqueue Jobs | Add shell-based tasks to the job queue |
| Worker Processes | One or more workers can process jobs in parallel |
| Automatic Retries | Failed jobs retry with exponential backoff |
| Dead Letter Queue | Jobs exceeding max retries are moved to `dead` state |
| Persistent Storage | SQLite ensures state is saved across restarts |
| Configurable Behavior | `max_retries`, `backoff_base`, etc. adjustable through CLI |
| Graceful Worker Shutdown | Workers finish running jobs before stopping |

---

## 🧩 Architecture Overview
<img width="1024" height="1024" alt="architecturre" src="https://github.com/user-attachments/assets/2d2d35cc-0bd7-4c9a-827d-cd5890044601" />











### Job Lifecycle

| State | Meaning |
|-------|---------|
| `pending` | Waiting to be picked by a worker |
| `processing` | Currently being executed |
| `completed` | Job finished successfully |
| `pending` (again) | Job failed but will retry after backoff |
| `dead` | Job exceeded retries and moved to DLQ |

---

## 📦 Installation (Google Colab Compatible)

```bash
cd queuectl/
pip install -e .


**💾 Data Persistence**

All job metadata is stored in SQLite (queue.db)

WAL mode ensures safe concurrent worker access

Jobs persist across notebook restarts or system reboot


**
⚙ Assumptions & Trade-offs**
Area: Decision
Storage: SQLite chosen for simplicity and durability
Concurrency: BEGIN IMMEDIATE ensures only one worker claims a job
Scheduling: Retry delays handled via due_at timestamps
Logging: Simple output/error stored in last_error for failed jobs


**🏁 Conclusion
**
This implementation provides a clean, durable, concurrency-safe background job queue system with:

Multiple workers

Retry backoff

DLQ recovery

Persistent job state

Simple & intuitive CLI

Ready to deploy and extend.


