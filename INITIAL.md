## FEATURE:

Implement the v5.1 “Video Production System” end-to-end, elevating the existing v5 blueprint into a production‑ready, phased rollout with operational maturity. Your AI agent should scaffold, configure, and deploy all five phases (Foundation, Processing, Intake & E2E, Resilience, Go‑Live) on Google Cloud, wiring together:

- **Phase 1 (Weeks 1–2):**

  - GCP project & API enablement
  - Service account + least‑privilege IAM
  - Drive folder structure & sharing
  - Firestore config+state initialization
  - Pub/Sub topics + DLQ setup

- **Phase 2 (Weeks 3–5):**

  - `processor-service` (Cloud Run + FFmpeg/OpenCV/Librosa)
  - `intelligence-service` (Cloud Run + Gemini API metadata)
  - Local unit & integration tests

- **Phase 3 (Weeks 6–7):**

  - `intake-service` (Cloud Function + polling Scheduler)
  - `intake-scheduler` (Cloud Scheduler)
  - `upload-scheduler` (n8n on e2‑micro)
  - First full system test end‑to‑end

- **Phase 4 (Weeks 8–9):**

  - Cloud Monitoring alerts for DLQ & error rates
  - Looker Studio status dashboard (processing queue, logs, failures)
  - Human‑in‑the‑loop retry Function + documented runbook

- **Phase 5 (Week 10+):**
  - Final IAM & cost review
  - Go‑live with real content
  - Ongoing monitoring, tuning via Firestore `config.json`
  - Iterative feature additions (e.g. new social platforms)

## EXAMPLES:

- `examples/drive_setup.py` — patterns for Drive folder polling
- `examples/pubsub_producer.py` — Pub/Sub message publishing
- `examples/cloud_run_template.py` — Cloud Run service scaffold
- `examples/n8n_workflow.json` — n8n upload‑scheduler stub

## DOCUMENTATION:

- **Google Drive + Scheduler:**  
  https://cloud.google.com/scheduler/docs  
  https://developers.google.com/drive/api/v3/reference/files/list
- **Firestore:**  
  https://cloud.google.com/firestore/docs/model/data-model
- **Pub/Sub & DLQ:**  
  https://cloud.google.com/pubsub/docs/topics  
  https://cloud.google.com/pubsub/docs/dead-letter
- **Cloud Run:**  
  https://cloud.google.com/run/docs/deploying
- **Cloud Functions:**  
  https://cloud.google.com/functions/docs/calling/cloud-scheduler
- **n8n on GCE:**  
  https://docs.n8n.io/reference/self-hosted-deployment
- **Monitoring & Alerts:**  
  https://cloud.google.com/monitoring/alerts
- **Looker Studio:**  
  https://support.google.com/looker-studio

## OTHER CONSIDERATIONS:

- **Configuration:**

  - One `config.json` in Firestore (fields: `youtube_daily_cap`, `tiktok_daily_cap`, algorithm weights, retry limits)
  - All services read settings at startup

- **Error Handling & Retry:**

  - Pub/Sub subscriptions use DLQ after 5 attempts
  - Manual retry Function takes `videoId`, re‑publishes `video.received`

- **Security & IAM:**

  - Principle‑of‑Least‑Privilege: service‑specific roles
  - Drive folder ACLs limited to Service Account only

- **Testing:**

  - Unit tests for each component (success, edge, fail) in `/tests`
  - Integration test that publishes a dummy message and tracks it through all services

- **CI/CD:**

  - `ruff --fix && mypy .`
  - `pytest tests/ -q`
  - Terraform `plan` check on infra changes

- **Operational Alerts:**
  - Alert on any message in DLQ
  - Alert on > 5% error rate across Cloud Run services
  - Notifications via email or Slack webhook
