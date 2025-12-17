# Autonomous Task AI

> **The Machine Does the Work**

---

## Overview

Autonomous Tasks let you describe what you want and the system builds it. No coding required - just describe your application in plain language.

**You say:**
> "Create a CRM for my cellphone store"

**You get:**
- Working HTMX application at `/apps/cellphone-crm`
- Database tables: `customers`, `products`, `sales`, `repairs`
- Forms, lists, search, filters - all functional
- Direct connection to botserver API

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         Your App                                 │
│                                                                  │
│   ┌──────────┐    ┌──────────┐    ┌──────────┐                 │
│   │  Forms   │    │  Lists   │    │  Actions │                 │
│   └────┬─────┘    └────┬─────┘    └────┬─────┘                 │
│        │               │               │                        │
│        └───────────────┼───────────────┘                        │
│                        │ HTMX                                   │
└────────────────────────┼────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────────┐
│                      botserver API                               │
│                                                                  │
│   /api/db/*          /api/drive/*         /api/llm/*           │
│   CRUD operations    File storage         AI features           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────────┐
│              PostgreSQL + MinIO + LLM                           │
│              (user_data virtual table)                          │
└─────────────────────────────────────────────────────────────────┘
```

**Key insight:** Apps talk directly to botserver. No middleware, no generated backend code - just HTMX calling the API.

---

## The user_data Virtual Table

All app data lives in one flexible table system:

```
App: cellphone-crm
Table: customers
     │
     ▼
Namespace: cellphone-crm.customers
     │
     ▼
Storage: user_data table with proper indexing
```

Your app calls `/api/db/customers` and botserver handles the rest.

### Benefits

- **No migrations** - Tables created on demand
- **Isolation** - Each app's data is separate
- **Flexibility** - Add fields anytime
- **Security** - Per-app access control

---

## How It Works

### 1. Describe

Tell the system what you want:

```
"Create a CRM for my cellphone store with:
- Customer tracking (name, phone, email)
- Product inventory with stock levels
- Sales linked to customers
- Repair status board"
```

### 2. Plan

System creates execution steps:

```
Step 1: Create tables (customers, products, sales, repairs)
Step 2: Generate HTMX application
Step 3: Add search and filters
Step 4: Configure repair workflow
```

### 3. Execute

Each step runs and shows progress:

```
[████████████████░░░░] 75%
Step 3 of 4: Adding search...
```

### 4. Deliver

Your app is ready:

```
✅ Application: /apps/cellphone-crm
✅ Tables: customers, products, sales, repairs
✅ Features: CRUD, search, status board
```

---

## Generated App Structure

```
.gbdrive/apps/cellphone-crm/
├── index.html          # HTMX application
├── _assets/
│   ├── htmx.min.js     # HTMX library
│   ├── app.js          # Helpers
│   └── styles.css      # Styling
└── schema.json         # Table definitions
```

---

## HTMX Patterns

### List with Auto-Refresh

```html
<div id="customers"
     hx-get="/api/db/customers"
     hx-trigger="load, every 30s"
     hx-swap="innerHTML">
    Loading...
</div>
```

### Create Form

```html
<form hx-post="/api/db/customers"
      hx-target="#customers"
      hx-swap="afterbegin">
    <input name="name" required>
    <input name="phone">
    <button type="submit">Add</button>
</form>
```

### Search

```html
<input type="search"
       hx-get="/api/db/customers"
       hx-trigger="keyup changed delay:300ms"
       hx-target="#customers"
       placeholder="Search...">
```

### Delete

```html
<button hx-delete="/api/db/customers/${id}"
        hx-target="closest tr"
        hx-confirm="Delete?">
    🗑️
</button>
```

---

## API Mapping

| HTMX | Endpoint | Action |
|------|----------|--------|
| `hx-get` | `/api/db/customers` | List |
| `hx-get` | `/api/db/customers/123` | Get one |
| `hx-post` | `/api/db/customers` | Create |
| `hx-put` | `/api/db/customers/123` | Update |
| `hx-delete` | `/api/db/customers/123` | Delete |

### Query Parameters

```
?q=john              # Search
?status=active       # Filter
?sort=created_at     # Sort
?order=desc          # Direction
?limit=20&offset=40  # Pagination
```

---

## Task Steps Storage

Every task stores its steps for:

- **Continuation** - Resume if interrupted
- **Progress** - Know exactly where you are
- **Debugging** - See what happened

```json
{
  "task_id": "abc123",
  "steps": [
    {"order": 1, "name": "Create tables", "status": "completed"},
    {"order": 2, "name": "Generate UI", "status": "running", "progress": 60},
    {"order": 3, "name": "Add search", "status": "pending"}
  ]
}
```

---

## Execution Modes

| Mode | Behavior |
|------|----------|
| **Automatic** | Runs without stopping |
| **Supervised** | Pauses before each step |
| **Dry Run** | Shows what would happen |

---

## Dev Chat Widget

Test your app without leaving the page:

1. Add `?dev=1` to URL or run on localhost
2. Click the floating chat icon (or Ctrl+Shift+D)
3. Talk to modify your app in real-time

```html
<script src="/_assets/dev-chat.js"></script>
```

The dev chat uses the same `user_data` system for history storage.

---

## Example: Cellphone Store CRM

**Request:**
> "CRM for cellphone store with customers, products, sales, and repair tracking"

**Result:**

| Table | Fields |
|-------|--------|
| `customers` | id, name, phone, email, notes |
| `products` | id, name, brand, model, price, stock |
| `sales` | id, customer_id, product_id, quantity, total |
| `repairs` | id, customer_id, device, status, price |

**Features:**
- Customer list with search
- Product inventory with stock alerts
- Sales entry form
- Repair status board (Kanban)

**Access:** `/apps/cellphone-crm`

---

## Best Practices

### Be Specific

✅ Good:
> "CRM for cellphone store with customer tracking, sales, and repair status workflow"

❌ Vague:
> "Make an app"

### Include Workflows

✅ Good:
> "Repair status: received → diagnosing → repairing → ready → delivered"

❌ Missing:
> "Track repairs"

### Mention Relationships

✅ Good:
> "Sales linked to customers and products"

❌ Unclear:
> "Sales tracking"

---

## See Also

- [Autonomous Tasks Chapter](../21-autonomous-tasks/README.md) - Complete guide
- [CREATE SITE](../06-gbdialog/keyword-create-site.md) - The keyword behind it
- [REST API](../10-rest/README.md) - API reference
- [HTMX Architecture](../04-gbui/htmx-architecture.md) - Frontend patterns