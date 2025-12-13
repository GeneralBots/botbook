# Autonomous Task AI

> **The Machine Does the Work**

---

<img src="../assets/chapter-07/autonomous-task-flow.svg" alt="Autonomous Task AI Flow" style="max-width: 100%; height: auto;">

---

## Overview

General Bots transforms how work gets done. Instead of humans executing tasks step-by-step, you describe what you want and the AI autonomously builds, deploys, and manages everything.

**Traditional approach:**
```
Human thinks → Human plans → Human codes → Human deploys → Human maintains
```

**General Bots approach:**
```
Human describes intent → AI plans → AI generates → AI deploys → AI monitors
```

This is not just task automation - it's **autonomous task execution** where the LLM acts as the brain that understands, plans, and accomplishes complex work.

---

## Core Architecture

### The Foundation: .gbai + .gbdrive

Every autonomous task operates within the General Bots package structure:

```
project.gbai/                    # The AI workspace
├── project.gbdialog/            # BASIC scripts (auto-generated)
│   ├── start.bas                # Entry point
│   └── tools/                   # Generated tools
├── project.gbkb/                # Knowledge base
│   └── docs/                    # Reference documents
├── project.gbot/                # Configuration
│   └── config.csv               # Bot settings
├── project.gbdrive/             # Online storage (MinIO bucket)
│   ├── assets/                  # Generated assets
│   ├── data/                    # Task data files
│   └── output/                  # Produced artifacts
└── project.gbtheme/             # UI customization
```

**Key insight:** The `.gbdrive` folder is a live link to cloud storage (MinIO/S3). Everything the AI creates, processes, or outputs lives here - accessible via API, web UI, or direct bucket access.

---

## How Autonomous Tasks Work

### 1. Intent Compilation

When you describe what you want, the LLM performs **intent compilation**:

```
User: "Create a CRM for tracking real estate leads with email automation"

LLM Analysis:
├── Action: CREATE
├── Target: CRM application
├── Domain: Real estate
├── Features:
│   ├── Lead tracking
│   ├── Email automation
│   └── Contact management
├── Integrations: Email service
└── Output: HTMX web application
```

### 2. Plan Generation

The AI generates an execution plan with ordered steps:

| Step | Priority | Description | Keywords |
|------|----------|-------------|----------|
| 1 | CRITICAL | Create database schema | NEW_TABLE, COLUMN |
| 2 | HIGH | Setup authentication | OAUTH, JWT |
| 3 | HIGH | Build lead management UI | CREATE SITE, FORM |
| 4 | MEDIUM | Create email templates | CREATE DRAFT |
| 5 | MEDIUM | Setup automation rules | SET SCHEDULE, ON |
| 6 | LOW | Deploy and configure | DEPLOY |

### 3. Autonomous Execution

The system executes each step, pausing only for:
- High-risk operations requiring approval
- Decisions that need human input
- External integrations requiring credentials

---

## CREATE SITE: The App Generator

`CREATE SITE` is the cornerstone keyword for autonomous app creation. It generates complete HTMX-based web applications bound to the botserver API.

### How It Works

```basic
CREATE SITE "crm", "bottemplates/apps/crud", "Build a real estate CRM with lead tracking"
```

**Execution flow:**

1. **Template Loading**
   - Reads HTML templates from `bottemplates/apps/crud/`
   - Combines all `.html` files as reference
   - Extracts HTMX patterns and component structures

2. **LLM Generation**
   - Sends combined templates + prompt to LLM
   - Generates new `index.html` with:
     - HTMX attributes for dynamic behavior
     - API bindings to botserver endpoints
     - CSS using local `_assets` only (no external CDNs)

3. **Deployment**
   - Creates folder at `<site_path>/crm/`
   - Writes generated `index.html`
   - Copies required assets
   - Site immediately available at `/crm`

### Generated App Structure

```
sites/crm/
├── index.html              # LLM-generated HTMX app
├── _assets/
│   ├── htmx.min.js         # HTMX library
│   ├── app.js              # Custom interactions
│   └── styles.css          # Themed styles
└── api/                    # Handled by botserver
```

### HTMX + GB API Pattern

Generated apps use HTMX to communicate with botserver:

```html
<!-- Lead list with live updates -->
<div id="leads"
     hx-get="/api/crm/leads"
     hx-trigger="load, every 30s"
     hx-swap="innerHTML">
    Loading leads...
</div>

<!-- Add new lead form -->
<form hx-post="/api/crm/leads"
      hx-target="#leads"
      hx-swap="afterbegin"
      hx-indicator="#saving">
    <input name="name" placeholder="Lead name" required>
    <input name="email" type="email" placeholder="Email">
    <input name="phone" placeholder="Phone">
    <button type="submit">
        <span class="btn-text">Add Lead</span>
        <span id="saving" class="htmx-indicator">Saving...</span>
    </button>
</form>

<!-- Lead detail with inline editing -->
<div class="lead-card"
     hx-get="/api/crm/leads/${id}"
     hx-trigger="click"
     hx-target="#detail-panel">
    <h3>${name}</h3>
    <p>${email}</p>
</div>
```

### API Binding

The generated HTMX calls map to botserver endpoints automatically:

| HTMX Call | Botserver Handler | BASIC Equivalent |
|-----------|-------------------|------------------|
| `GET /api/crm/leads` | Query handler | `FIND "leads"` |
| `POST /api/crm/leads` | Insert handler | `UPSERT "leads"` |
| `PUT /api/crm/leads/:id` | Update handler | `SET "leads"` |
| `DELETE /api/crm/leads/:id` | Delete handler | `DELETE "leads"` |

---

## The .gbdrive Workspace

Every autonomous task uses `.gbdrive` as its workspace - a cloud-synced folder structure:

### Storage Architecture

```
.gbdrive/ (MinIO bucket)
├── tasks/
│   ├── task-001/
│   │   ├── plan.json           # Execution plan
│   │   ├── progress.json       # Current state
│   │   ├── logs/               # Execution logs
│   │   └── output/             # Generated files
│   └── task-002/
│       └── ...
├── apps/
│   ├── crm/
│   │   ├── index.html
│   │   └── _assets/
│   └── dashboard/
│       └── ...
├── data/
│   ├── leads.json
│   ├── contacts.json
│   └── reports/
└── assets/
    ├── templates/
    ├── images/
    └── documents/
```

### Accessing .gbdrive

**Via API:**
```javascript
// List files
fetch('/api/drive/list?path=tasks/task-001')

// Download file
fetch('/api/drive/download?path=apps/crm/index.html')

// Upload file
fetch('/api/drive/upload', {
    method: 'POST',
    body: formData
})
```

**Via BASIC:**
```basic
' List drive contents
files = DIR ".gbdrive/tasks"

' Copy to drive
COPY "report.pdf" TO ".gbdrive/output/"

' Read from drive
data = LOAD ".gbdrive/data/leads.json"
```

**Via rclone:**
```bash
# Sync local to drive
rclone sync ./mybot.gbai drive:mybot --watch

# Download from drive
rclone copy drive:mybot/output ./local-output
```

---

## Execution Modes

### Semi-Automatic (Recommended)

The AI executes autonomously but pauses for critical decisions:

```
[Step 1] Creating database... ✓
[Step 2] Setting up auth... ✓
[Step 3] Building UI... ✓
[Step 4] ⚠️ APPROVAL REQUIRED
         Action: Send 500 welcome emails
         Impact: Email quota usage
         [Approve] [Modify] [Skip]
```

### Supervised

Every step requires explicit approval:

```
[Step 1] Create database schema
         Tables: leads, contacts, activities
         [Approve] [Modify] [Skip]
```

### Fully Automatic

Complete autonomous execution without stops:

```
Task: "Build CRM for real estate"
Status: RUNNING
Progress: ████████████░░░░ 75%
Current: Generating email templates
ETA: 12 minutes
```

### Dry Run

Simulates execution without making changes:

```
[SIMULATION] Step 1: Would create 3 tables
[SIMULATION] Step 2: Would generate 5 HTML files
[SIMULATION] Step 3: Would create 2 email templates
[SIMULATION] Estimated cost: $0.45
[SIMULATION] Estimated time: 25 minutes

Proceed with actual execution? [Yes] [No]
```

---

## Generated BASIC Programs

Behind every autonomous task is a BASIC program. The LLM generates executable code:

```basic
' =============================================================================
' AUTO-GENERATED: Real Estate CRM
' Created: 2024-01-15
' =============================================================================

PLAN_START "Real Estate CRM", "Lead tracking with email automation"
  STEP 1, "Create database", CRITICAL
  STEP 2, "Build UI", HIGH
  STEP 3, "Setup automation", MEDIUM
PLAN_END

' -----------------------------------------------------------------------------
' STEP 1: Database Schema
' -----------------------------------------------------------------------------

NEW_TABLE "leads"
  COLUMN "id", UUID, PRIMARY KEY
  COLUMN "name", STRING, REQUIRED
  COLUMN "email", STRING
  COLUMN "phone", STRING
  COLUMN "status", STRING, DEFAULT "new"
  COLUMN "source", STRING
  COLUMN "created_at", TIMESTAMP
SAVE_TABLE

NEW_TABLE "activities"
  COLUMN "id", UUID, PRIMARY KEY
  COLUMN "lead_id", UUID, FOREIGN KEY "leads.id"
  COLUMN "type", STRING
  COLUMN "notes", TEXT
  COLUMN "created_at", TIMESTAMP
SAVE_TABLE

' -----------------------------------------------------------------------------
' STEP 2: Generate Application
' -----------------------------------------------------------------------------

CREATE SITE "crm", "bottemplates/apps/crud", "Real estate CRM with:
- Lead list with filtering and search
- Lead detail view with activity timeline
- Quick add form
- Status pipeline view (Kanban)
- Email integration buttons"

' -----------------------------------------------------------------------------
' STEP 3: Automation Rules
' -----------------------------------------------------------------------------

ON "leads" INSERT DO
  ' Send welcome email to new leads
  IF NEW.email != "" THEN
    CREATE DRAFT NEW.email, "Welcome to Our Service", "
      Hi " + NEW.name + ",
      Thank you for your interest...
    "
  END IF
  
  ' Log activity
  UPSERT "activities"
    SET lead_id = NEW.id
    SET type = "created"
    SET notes = "Lead created from " + NEW.source
END ON

' Schedule daily digest
SET SCHEDULE "0 9 * * *" DO
  leads = FIND "leads", "status=new AND created_at > yesterday"
  IF COUNT(leads) > 0 THEN
    report = LLM "Create summary of " + COUNT(leads) + " new leads"
    SEND MAIL "sales@company.com", "Daily Lead Digest", report
  END IF
END SCHEDULE
```

---

## Task Lifecycle

### States

| State | Description |
|-------|-------------|
| `draft` | Task created, intent captured |
| `compiling` | LLM generating execution plan |
| `ready` | Plan generated, awaiting execution |
| `running` | Currently executing steps |
| `paused` | Execution paused by user |
| `pending_approval` | Waiting for approval on high-risk step |
| `waiting_decision` | Needs user input to continue |
| `completed` | Successfully finished all steps |
| `failed` | Encountered unrecoverable error |
| `cancelled` | Stopped by user |

### Monitoring

Real-time task monitoring via WebSocket:

```javascript
// Connect to task updates
const ws = new WebSocket('wss://host/ws/autotask');

ws.onmessage = (event) => {
    const data = JSON.parse(event.data);
    switch (data.type) {
        case 'step_progress':
            updateProgressBar(data.progress);
            break;
        case 'approval_required':
            showApprovalDialog(data.approval);
            break;
        case 'task_completed':
            showSuccessNotification(data.task);
            break;
    }
};
```

---

## Building Your Own Autonomous Workflows

### Example: Automated Report Generator

```basic
' Intent: "Generate weekly sales report every Monday"

SET SCHEDULE "0 8 * * 1" DO
  ' Gather data
  sales = FIND "orders", "created_at > last_week"
  customers = FIND "customers", "orders > 0"
  
  ' Generate analysis
    analysis = LLM "Analyze sales data: " + JSON(sales)
  
    ' Create report site
    CREATE SITE "report-" + TODAY(), "bottemplates/apps/dashboard", analysis
  
  ' Notify stakeholders
  SEND MAIL "team@company.com", "Weekly Sales Report", "
    Report ready: /report-" + TODAY()
  "
END SCHEDULE
```

### Example: Customer Onboarding Automation

```basic
' Triggered when new customer signs up
ON "customers" INSERT DO
  ' Create personalized welcome site
  welcome_content = LLM "Create welcome page for " + NEW.name + " in " + NEW.industry
  CREATE SITE "welcome-" + NEW.id, "bottemplates/apps/crud", welcome_content
  
  ' Schedule follow-up sequence
  CREATE TASK "Follow up with " + NEW.name, "Call in 3 days"
  
  ' Send welcome email with site link
  CREATE DRAFT NEW.email, "Welcome!", "
    Hi " + NEW.name + ",
    Your personalized portal is ready: /welcome-" + NEW.id
  "
END ON
```

### Example: Dynamic Dashboard Builder

```basic
' User asks: "Create a dashboard showing our KPIs"

' Step 1: Analyze available data
tables = SHOW TABLES
schema = LLM "Analyze schema for KPI opportunities: " + JSON(tables)

' Step 2: Generate dashboard
CREATE SITE "dashboard", "bottemplates/apps/dashboard", "
  Create executive dashboard with:
  " + schema + "
  
  Include:
  - Real-time metrics cards
  - Trend charts (last 30 days)
  - Comparison to previous period
  - Export to PDF button
"

' Step 3: Set auto-refresh
TALK "Dashboard created at /dashboard with live updates"
```

---

## Integration with GB Infrastructure

### How Apps Use botserver

Generated HTMX apps don't need their own backend - they use botserver's API:

```
┌─────────────────────────────────────────────────────────────┐
│                    Generated HTMX App                        │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐       │
│  │  Forms  │  │  Lists  │  │ Charts  │  │ Actions │       │
│  └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘       │
│       │            │            │            │              │
│       └────────────┴────────────┴────────────┘              │
│                         │ HTMX                              │
└─────────────────────────┼───────────────────────────────────┘
                          │
┌─────────────────────────┼───────────────────────────────────┐
│                    botserver API                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │   CRUD   │  │   LLM    │  │  Drive   │  │   Mail   │   │
│  │ /api/db  │  │ /api/llm │  │/api/drive│  │/api/mail │   │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘   │
│       │             │             │             │           │
│  ┌────┴─────────────┴─────────────┴─────────────┴────┐     │
│  │              PostgreSQL + MinIO + LLM              │     │
│  └────────────────────────────────────────────────────┘     │
└─────────────────────────────────────────────────────────────┘
```

### Available API Endpoints

| Endpoint | Purpose | HTMX Usage |
|----------|---------|------------|
| `/api/db/{table}` | CRUD operations | `hx-get`, `hx-post`, `hx-put`, `hx-delete` |
| `/api/llm/complete` | LLM generation | `hx-post` with prompt |
| `/api/drive/*` | File operations | `hx-get` for download, `hx-post` for upload |
| `/api/mail/send` | Email sending | `hx-post` with recipients |
| `/api/chat` | Conversational AI | WebSocket |

---

## Best Practices

### Writing Effective Intents

**Good:**
```
"Create a project management app for our marketing team with:
- Kanban board for campaign tasks
- Team member assignment
- Deadline tracking with reminders
- File attachments per task
- Weekly progress reports"
```

**Bad:**
```
"Make an app"
```

### Template Organization

Keep templates organized for reuse:

```
templates/
├── app/                    # Full application templates
│   ├── dashboard.html
│   ├── crud-list.html
│   └── form-wizard.html
├── components/             # Reusable components
│   ├── data-table.html
│   ├── chart-card.html
│   └── form-field.html
├── emails/                 # Email templates
│   ├── welcome.html
│   └── notification.html
└── reports/                # Report templates
    ├── summary.html
    └── detailed.html
```

### Security Considerations

- All generated apps inherit botserver authentication
- API calls require valid session tokens
- File uploads go through virus scanning
- Database operations respect row-level security
- LLM outputs are sanitized before rendering

---

## See Also

- [CREATE SITE Keyword](../06-gbdialog/keyword-create-site.md) - Detailed syntax
- [.gbai Architecture](../02-templates/gbai.md) - Package structure
- [.gbdrive Storage](../02-templates/gbdrive.md) - File management
- [HTMX Architecture](../04-gbui/htmx-architecture.md) - UI patterns
- [API Reference](../10-rest/README.md) - botserver endpoints