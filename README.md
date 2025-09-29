# Go Job Queue + Cache 🚀

A lightweight **distributed job queue system in Go** with:
- **REST APIs** for enqueueing jobs and checking status  
- **Worker pool** for concurrent job execution  
- **Retries** with exponential backoff  
- **LRU + TTL cache** for fast job result lookups  
- **Metrics endpoint** for monitoring queue health  

👉 Think of it as a **mini Sidekiq/Celery**, but simple, fast, and Go-native.

---

## ✨ Features

✅ REST API  
- `POST /enqueue` → Add a new job with payload (e.g., “send email”, “resize image”).  
- `GET /status/{jobID}` → Get job state + result.  

✅ Job Queue  
- In-memory + persistent queue (Postgres/SQLite).  
- Worker pool with configurable concurrency.  
- Retries with exponential backoff.  
- Dead-letter queue for failed jobs.  

✅ Caching  
- In-memory LRU + TTL cache for recent job results.  
- Example: Keep last 1000 jobs cached for 5 minutes.  
- Cache hit/miss metrics.  

✅ Metrics  
- Prometheus `/metrics` endpoint.  
- Exposes: jobs enqueued, succeeded, failed, retried, cache hits/misses.  

✅ Extensible  
- Add custom job handlers (e.g., email, file processing, API calls).  
- Pluggable storage (SQLite/Postgres → future Redis/S3).  

---

## 💡 Use Cases

This system is ideal for teams/startups who need **background processing** without the overhead of Kafka/RabbitMQ/Celery:

- **Email Sending Service**  
  Enqueue “send email” jobs → workers handle retries if SMTP fails.  

- **Image Processing / File Conversion**  
  Enqueue “resize image” → workers process → results cached for quick retrieval.  

- **ETL Jobs / Data Pipelines**  
  Run scheduled jobs (daily reports, log cleanup, DB migrations).  

- **API Offloading**  
  Accept heavy API requests → enqueue → return jobID → client checks result later.  

---

## 🚀 Roadmap

- [x] REST APIs (`/enqueue`, `/status/{id}`)  
- [x] Worker pool (concurrent job execution)  
- [x] Retries with exponential backoff  
- [x] LRU + TTL cache for job results  
- [ ] Dead-letter queue  
- [ ] Dashboard (TUI or Next.js)  
- [ ] K8s deployment manifests  

---

## 🛠️ Quickstart (coming soon)

```bash
git clone https://github.com/<your-username>/go-job-queue-cache
cd go-job-queue-cache
go run main.go
