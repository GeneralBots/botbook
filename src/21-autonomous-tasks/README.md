# Autonomous Tasks

> **From Intent to Application**

---

## What Are Autonomous Tasks?

Autonomous Tasks transform how applications are built. Instead of writing code manually, you describe what you want, and the system generates a complete working application.

**Example:**
> "I want to create a CRM for my cellphone store"

**Result:**
- A fully functional HTMX web application at `/apps/cellphone-crm`
- Database tables for `customers`, `products`, `sales`, `repairs`
- Forms, lists, filters, and reports - all working
- Connected to your bot for AI-assisted operations

---

## How It Works

```
┌─────────────────────────────────────────────────────────────────┐
│  1. DESCRIBE                                                     │
│     "Create a CRM for my cellphone store with customer          │
│      tracking, sales, and repair status"                        │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  2. PLAN                                                         │
│     ┌──────────────┐ ┌──────────────┐ ┌──────────────┐         │
│     │ Step 1       │ │ Step 2       │ │ Step 3       │         │
│     │ Create       │→│ Generate     │→│ Setup        │         │
│     │ Tables       │ │ UI           │ │ Workflows    │         │
│     └──────────────┘ └──────────────┘ └──────────────┘         │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  3. EXECUTE                                                      │
│     [████████████████░░░░░░░░░░] 60% - Generating UI...         │
│     Step 2 of 3 • ETA: 2 minutes                                │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  4. DONE                                                         │
│     ✅ Application ready at /apps/cellphone-crm                 │
│     ✅ Tables created: customers, products, sales, repairs      │
│     ✅ AI assistant connected                                    │
└─────────────────────────────────────────────────────────────────┘
```

---

## The Stack

| Layer | Technology | What It Does |
|-------|------------|--------------|
| **Frontend** | HTMX | Dynamic UI without writing JavaScript |
| **Backend** | botserver | API, authentication, business logic |
| **Database** | PostgreSQL | Stores your application data |
| **Storage** | MinIO/S3 | Files, documents, uploads |
| **AI** | LLM | Generates the app, powers the assistant |

### No Middleware Needed

Generated apps talk directly to botserver:

```
┌─────────────────────┐      ┌─────────────────────┐
│   HTMX Frontend     │──────│     botserver       │
│                     │ HTTP │                     │
│  - Forms            │◄────►│  - /api/db/table    │
│  - Lists            │      │  - /api/drive/...   │
│  - Actions          │      │  - /api/llm/...     │
└─────────────────────┘      └─────────────────────┘
```

---

## Where Apps Live

Generated applications are stored in `.gbdrive/apps`:

```
mybot.gbai/
└── mybot.gbdrive/
    └── apps/
        └── cellphone-crm/
            ├── index.html      # Main application
            ├── _assets/
            │   ├── htmx.min.js
            │   ├── app.js
            │   └── styles.css
            └── data/
                └── schema.json  # Table definitions
```

Access your app at: `https://your-bot.com/apps/cellphone-crm`

---

## Data Storage

### The `user_data` Virtual Table

Every app has access to a flexible data store through the `user_data` virtual table system. When your app needs a table like `customers`, botserver maps it to the underlying storage:

```
App request: POST /api/db/customers
     │
     ▼
botserver routes to: user_data table with namespace "cellphone-crm.customers"
     │
     ▼
PostgreSQL storage with proper indexing and relationships
```

### Your Tables Are Real

When you create an app that needs `customers`, `products`, and `sales` tables, they're created as proper database entities:

| Table | Fields | Purpose |
|-------|--------|---------|
| `customers` | id, name, phone, email, notes | Customer records |
| `products` | id, name, brand, model, price, stock | Inventory |
| `sales` | id, customer_id, product_id, date, amount | Transactions |
| `repairs` | id, customer_id, device, status, notes | Service tracking |

---

## Task Steps

Every task is broken into steps that are stored for:

1. **Continuation** - Resume later if interrupted
2. **Progress tracking** - See exactly where you are
3. **Debugging** - Understand what happened
4. **Learning** - Improve future generations

### Step Structure

```json
{
  "task_id": "abc123",
  "steps": [
    {
      "order": 1,
      "name": "Create database tables",
      "status": "completed",
      "started_at": "2024-01-15T10:00:00Z",
      "completed_at": "2024-01-15T10:00:15Z"
    },
    {
      "order": 2,
      "name": "Generate application UI",
      "status": "running",
      "started_at": "2024-01-15T10:00:16Z",
      "progress": 60
    },
    {
      "order": 3,
      "name": "Configure workflows",
      "status": "pending"
    }
  ]
}
```

---

## Chapter Contents

- [Task Workflow](./workflow.md) - From intent to completion
- [App Generation](./app-generation.md) - How apps are created
- [Data Model](./data-model.md) - Tables and storage
- [Progress Tracking](./progress.md) - Monitoring and continuation
- [Examples](./examples.md) - Real-world autonomous tasks

---

## Quick Example

**You say:**
> "Create a CRM for my cellphone store with customers, sales tracking, and repair status"

**The system:**

1. **Analyzes your intent:**
   - Type: CRM application
   - Domain: Cellphone retail
   - Entities: customers, products, sales, repairs

2. **Creates the plan:**
   - Step 1: Create `customers`, `products`, `sales`, `repairs` tables
   - Step 2: Generate HTMX application with forms and lists
   - Step 3: Add search, filters, and status workflows

3. **Executes and reports:**
   ```
   ✅ Step 1: Tables created
   ⏳ Step 2: Generating UI... (60%)
   ⏸ Step 3: Waiting
   ```

4. **Delivers the app:**
   - URL: `/apps/cellphone-crm`
   - Features: Customer list, add customer form, sales tracking, repair status board

---

## See Also

- [CREATE SITE](../06-gbdialog/keyword-create-site.md) - The keyword behind app generation
- [.gbdrive Storage](../02-templates/gbdrive.md) - Where apps live
- [REST API](../10-rest/README.md) - The API your apps use
- [HTMX Architecture](../04-gbui/htmx-architecture.md) - Frontend patterns