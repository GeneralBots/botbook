# General Bots Complete Roadmap 2018-2026

## Merged Timeline: User Requirements + botbook Documentation

This table merges the proposed timeline with all features documented in botbook/src.

---

## Summary

| Period | Focus | Feature Count | Status |
|--------|-------|---------------|--------|
| 2018-2024 | v1-v5 Pre-LLM | 12 | ✅ Complete |
| 2024 | v6 Foundation | 8 | ✅ Complete |
| 2025 H1 | Rust Migration | 10 | ✅ Complete |
| 2025 H2 | Features & Tasks | 10 | ✅ Complete |
| 2026 Q1 | Autonomous GO | 12 | 📋 Planned |
| 2026 Q2 | Collaboration & AI | 14 | 📋 Planned |
| 2026 Q3 | Advanced Features | 6 | 📋 Planned |
| 2026 Q4 | Enterprise | 7 | 📋 Planned |
| **TOTAL** | | **79** | |

---

## 2018-2024: v1-v5 Pre-LLM Era ✅

| # | Feature | Source | Documentation |
|---|---------|--------|---------------|
| 1 | Package System (.gbai/.gbot/.gbkb/.gbdialog/.gbtheme) | Your list + botbook | 02-templates/ |
| 2 | TALK / HEAR Keywords | Your list + botbook | 06-gbdialog/keyword-talk.md |
| 3 | NLP / BERT Intent Recognition | Your list | 06-gbdialog/ |
| 4 | GPT-3.5 Integration | Your list | 08-config/llm-config.md |
| 5 | QR CODE Keyword | Your list + botbook | 06-gbdialog/keyword-qrcode.md |
| 6 | SET SCHEDULE Keyword | Your list + botbook | 06-gbdialog/keyword-set-schedule.md |
| 7 | LLM Keyword | Your list + botbook | 06-gbdialog/ |
| 8 | Node.js Core | Your list | Historical |
| 9 | Azure Bot Service | Your list + botbook | Historical |
| 10 | DirectLine API | botbook | Historical |
| 11 | MS Teams Bot | botbook | Historical |
| 12 | Web Server | botbook | Historical |

---

## 2024: v6 Rust Foundation ✅

| # | Feature | Source | Documentation |
|---|---------|--------|---------------|
| 1 | Migration v5 → v6 | Your list | 14-migration/ |
| 2 | Node.js → Rust Rewrite | Your list + botbook | 07-gbapp/architecture.md |
| 3 | New Rust Architecture | Your list + botbook | 07-gbapp/crates.md |
| 4 | Minimal Flow MVP | Your list | 07-gbapp/ |
| 5 | PostgreSQL + Diesel ORM | botbook | 15-appendix/schema.md |
| 6 | Auto-Bootstrap System | botbook | 01-introduction/ |
| 7 | Vault Secrets Management | botbook | 08-config/secrets-management.md |
| 8 | Basic HTMX UI | botbook | 04-gbui/htmx-architecture.md |

---

## 2025 H1: Rust Migration & Channels ✅

| # | Feature | Source | Documentation |
|---|---------|--------|---------------|
| 1 | BASIC Engine (70+ keywords) | Your list + botbook | 06-gbdialog/keywords.md |
| 2 | System Automation (cron) | Your list + botbook | 11-features/automation.md |
| 3 | Web Chat Channel | Your list + botbook | 04-gbui/apps/chat.md |
| 4 | LLM Integration (multi-provider) | Your list + botbook | 08-config/llm-config.md |
| 5 | Drive Storage (S3) | Your list + botbook | 02-templates/gbdrive.md |
| 6 | Email System (IMAP/SMTP) | Your list + botbook | 11-features/email.md |
| 7 | REST API | Your list + botbook | 10-rest/ |
| 8 | **Telegram Channel** | botbook | 11-features/channels.md |
| 9 | **PDF Generation** | botbook | 06-gbdialog/keyword-generate-pdf.md |
| 10 | **WhatsApp Channel** | botbook | 11-features/channels.md |

---

## 2025 H2: Features & Autonomous Tasks ✅

| # | Feature | Source | Documentation |
|---|---------|--------|---------------|
| 1 | Tasks AI Autonomous (AUTOTASK) | Your list + botbook | 07-gbapp/autonomous-tasks.md |
| 2 | Knowledge Base (Vector) | Your list + botbook | 03-knowledge-base/ |
| 3 | Vector Database (Qdrant) | Your list + botbook | 03-knowledge-base/vector-collections.md |
| 4 | Tools System (MCP) | Your list + botbook | 09-tools/ |
| 5 | UI Minimal Suite | Your list + botbook | 04-gbui/ |
| 6 | APP Generator | Your list + botbook | 07-gbapp/autonomous-tasks.md |
| 7 | **BOT Generator** | botbook | 07-gbapp/autonomous-tasks.md |
| 8 | **SITE Generator** | botbook | 06-gbdialog/keyword-create-site.md |
| 9 | **LANDPAGE Generator** | botbook | 07-gbapp/autonomous-tasks.md |
| 10 | **Analytics Dashboard** | botbook | 04-gbui/apps/analytics.md |

---

## 2026 Q1: Autonomous GO ⭐ FLAGSHIP 📋

| # | Feature | Source | Documentation |
|---|---------|--------|---------------|
| 1 | **Tasks AI GO** ⭐ | Your list + botbook | 07-gbapp/autonomous-tasks.md |
| 2 | Gmail Integration | Your list | 10-rest/email-api.md |
| 3 | Outlook/Hotmail | Your list | 10-rest/email-api.md |
| 4 | Google Drive | Your list | 08-config/drive.md |
| 5 | OneDrive | Your list | 08-config/drive.md |
| 6 | Google Calendar | Your list | 10-rest/calendar-api.md |
| 7 | Outlook Calendar | Your list | 10-rest/calendar-api.md |
| 8 | Speech to Text | Your list | 08-config/multimodal.md |
| 9 | Image Generation | Your list | 08-config/multimodal.md |
| 10 | Vision Analysis | Your list | 08-config/multimodal.md |
| 11 | **MS Teams Channel** | Your list + botbook | 11-features/channels.md |
| 12 | **Multi-Agent System** | Your list + botbook | 11-features/multi-agent-orchestration.md |

---

## 2026 Q2: Collaboration & AI Tools 📋

| # | Feature | Source | Documentation |
|---|---------|--------|---------------|
| 1 | **Paper App (AI Writing)** | botbook | 04-gbui/apps/paper.md |
| 2 | **Research App (AI Search)** | botbook | 04-gbui/apps/research.md |
| 3 | **Transfer to Human** | botbook | 11-features/transfer-to-human.md |
| 4 | **LLM-Assisted Attendant** (AI Copilot for Agents) | botbook | 11-features/attendant-llm-assist.md |
| 5 | Bot Marketplace | Your list | Future |
| 6 | Compliance Suite | Your list + botbook | 04-gbui/apps/compliance.md |
| 7 | Analytics Reports | Your list + botbook | 10-rest/analytics-api.md |
| 8 | **Slack Channel** | botbook | 11-features/channels.md |
| 9 | **Discord Channel** | botbook | 11-features/channels.md |
| 10 | **Google Sheets** | botbook | Future |
| 11 | **Excel Online** | botbook | Future |
| 12 | **Whiteboard Collaboration** | botbook | 10-rest/whiteboard-api.md |
| 13 | **Player App (Media)** | botbook | 04-gbui/apps/player.md |
| 14 | **Sources App (Prompts)** | botbook | 04-gbui/apps/sources.md |

---

## 2026 Q3: Advanced AI Features 📋

| # | Feature | Source | Documentation |
|---|---------|--------|---------------|
| 1 | Workflow Designer | Your list + botbook | 04-gbui/apps/designer.md |
| 2 | CRM Integration | Your list | 02-templates/template-crm.md |
| 3 | **Voice Synthesis (TTS)** | botbook | 08-config/multimodal.md |
| 4 | **ERP Integration** | botbook | 02-templates/template-erp.md |
| 5 | **Instagram Channel** | botbook | 11-features/channels.md |
| 6 | **SMS Channel** | botbook | 06-gbdialog/keyword-sms.md |

---

## 2026 Q4: Enterprise Scale 📋

| # | Feature | Source | Documentation |
|---|---------|--------|---------------|
| 1 | Mobile Apps (iOS/Android) | Your list + botbook | 13-devices/mobile.md |
| 2 | Enterprise SSO (SAML/OIDC) | Your list + botbook | 12-auth/ |
| 3 | **Backup & Restore** | botbook | 10-rest/backup-api.md |
| 4 | **NVIDIA GPU Support** | botbook | 09-tools/nvidia-gpu-setup.md |
| 5 | **Docker Deployment** | botbook | 07-gbapp/docker-deployment.md |
| 6 | **LXC Containers** | botbook | 07-gbapp/containers.md |
| 7 | **Advanced Monitoring** | botbook | 10-rest/monitoring-api.md |

---

## Suite Apps Status

| App | Category | Timeline | Documentation |
|-----|----------|----------|---------------|
| Chat | Core | 2025 H1 ✅ | 04-gbui/apps/chat.md |
| Drive | Storage | 2025 H1 ✅ | 04-gbui/apps/drive.md |
| Tasks | Productivity | 2025 H2 ✅ | 04-gbui/apps/tasks.md |
| Mail | Communication | 2025 H1 ✅ | 04-gbui/apps/mail.md |
| Calendar | Scheduling | 2026 Q1 📋 | 04-gbui/apps/calendar.md |
| Meet | Video | 2026 Q2 📋 | 04-gbui/apps/meet.md |
| Paper | AI Writing | 2026 Q2 📋 | 04-gbui/apps/paper.md |
| Research | AI Search | 2026 Q2 📋 | 04-gbui/apps/research.md |
| Analytics | Reports | 2025 H2 ✅ | 04-gbui/apps/analytics.md |
| Designer | Visual | 2026 Q3 📋 | 04-gbui/apps/designer.md |
| Sources | Prompts | 2026 Q2 📋 | 04-gbui/apps/sources.md |
| Compliance | Security | 2026 Q2 📋 | 04-gbui/apps/compliance.md |
| Player | Media | 2026 Q2 📋 | 04-gbui/apps/player.md |

---

## Channel Support Status

| Channel | Timeline | Documentation |
|---------|----------|---------------|
| Web Chat | 2025 H1 ✅ | 04-gbui/apps/chat.md |
| WhatsApp | 2025 H1 ✅ | 11-features/channels.md |
| Telegram | 2025 H1 ✅ | 11-features/channels.md |
| MS Teams | 2026 Q1 📋 | 11-features/channels.md |
| Slack | 2026 Q2 📋 | 11-features/channels.md |
| Discord | 2026 Q2 📋 | 11-features/channels.md |
| Instagram | 2026 Q3 📋 | 11-features/channels.md |
| SMS | 2026 Q3 📋 | 06-gbdialog/keyword-sms.md |

---

## Completed Features (Outside Roadmap)

| Feature | Status | Notes |
|---------|--------|-------|
| White Label | ✅ Complete | Branding customization available |

---

## Infrastructure Features

| Feature | Timeline | Documentation |
|---------|----------|---------------|
| PostgreSQL | 2024 ✅ | 15-appendix/schema.md |
| Redis Cache | 2024 ✅ | 07-gbapp/architecture.md |
| MinIO/S3 | 2024 ✅ | 08-config/drive.md |
| Qdrant Vector | 2025 H2 ✅ | 03-knowledge-base/ |
| Vault Secrets | 2024 ✅ | 08-config/secrets-management.md |
| NVIDIA GPU | 2026 Q4 📋 | 09-tools/nvidia-gpu-setup.md |
| Docker | 2026 Q4 📋 | 07-gbapp/docker-deployment.md |
| LXC | 2026 Q4 📋 | 07-gbapp/containers.md |

---

## Legend

- ✅ Complete
- 📋 Planned
- ⭐ Flagship Feature
- **Bold** = Added from botbook (missing from original timeline)