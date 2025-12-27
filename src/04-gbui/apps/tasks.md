# Tasks

> **Describe What You Want, Get a Working App**

---

## What is Tasks?

Tasks is where you describe what you want and the system builds it. No coding - just tell it what you need.

| You Say | You Get |
|---------|---------|
| "CRM for my cellphone store" | Working app with customers, sales, inventory |
| "Track repair status" | Kanban board with status workflow |
| "Sales dashboard" | Charts and metrics auto-updating |

---

## How It Works

```
DESCRIBE → PLAN → EXECUTE → DONE
```

### 1. Describe

Write what you want in plain language:

```
"Create a CRM for my cellphone store with:
- Customer list (name, phone, email)
- Product inventory with stock levels  
- Sales tracking
- Repair status board"
```

### 2. Plan

System shows the execution plan:

```
Step 1: Create tables (customers, products, sales, repairs)
Step 2: Generate application UI
Step 3: Add search and filters
Step 4: Configure repair workflow

Confidence: 92% | ETA: 3 minutes
```

### 3. Execute

Watch progress in real-time:

```
[████████████████░░░░] 75%
Step 3 of 4: Adding search...
```

### 4. Done

Your app is ready:

```
✅ Application: /apps/cellphone-crm
✅ Tables: customers, products, sales, repairs
```

---

## Creating a Task

### Write Your Intent

Be specific about what you want:

| ✅ Good | ❌ Too Vague |
|---------|--------------|
| "CRM for cellphone store with customer tracking and repair status" | "Make an app" |
| "Inventory with low stock alerts when below 10 units" | "Track stuff" |
| "Sales dashboard with daily revenue chart" | "Dashboard" |

### Choose Mode

| Mode | Best For |
|------|----------|
| **Automatic** | Trusted, simple tasks |
| **Supervised** | Learning, want to review each step |
| **Dry Run** | Testing - see what would happen |

### Click Execute

The system runs each step and shows progress.

---

## Task Progress

### Status Icons

| Icon | Meaning |
|------|---------|
| ✓ | Completed |
| ◐ | Running |
| ○ | Pending |
| ⚠ | Needs attention |
| ✕ | Failed |

### Steps Are Saved

Every step is stored so you can:

- **Resume** if interrupted
- **Track** exactly where you are
- **Debug** if something fails

---

## Your Generated App

Apps are created at `.gbdrive/apps/{name}/`:

```
.gbdrive/apps/cellphone-crm/
├── index.html      # Your application
├── _assets/
│   ├── htmx.min.js
│   └── styles.css
└── schema.json     # Table definitions
```

### Direct API Access

Your app talks directly to botserver:

```html
<!-- List customers -->
<div hx-get="/api/db/customers" hx-trigger="load">

<!-- Add customer -->
<form hx-post="/api/db/customers">

<!-- Search -->
<input hx-get="/api/db/customers" 
       hx-trigger="keyup changed delay:300ms">
```

No middleware - HTMX calls the API directly.

---

## Data Storage

All data uses the `user_data` virtual table:

```
Your app: cellphone-crm
Table: customers
     ↓
API: /api/db/customers
     ↓
Storage: user_data (namespaced)
```

### Benefits

- Tables created on demand
- Each app isolated
- Add fields anytime
- No migrations needed

---

## Task Actions

| Action | When | What It Does |
|--------|------|--------------|
| **Pause** | Running | Stop temporarily |
| **Resume** | Paused | Continue from where stopped |
| **Cancel** | Anytime | Stop and discard |
| **Retry** | Failed | Try failed step again |

---

## From Chat

Create tasks by talking to your bot:

**You:** "I need a CRM for my cellphone store"

**Bot:** "I'll create that. Here's the plan:
- 4 steps, ~3 minutes
- Tables: customers, products, sales, repairs

Execute?"

**You:** "Yes"

**Bot:** "Started. I'll notify you when done."

---

## Examples

### Cellphone Store CRM

```
"CRM with customers, products, sales, and repair tracking 
with status: received, diagnosing, repairing, ready, delivered"
```

### Restaurant Reservations

```
"Reservation system with tables, bookings, and waitlist"
```

### Inventory Tracker

```
"Inventory with products, suppliers, and low stock alerts"
```

---

## See Also

- [Autonomous Tasks](../../17-autonomous-tasks/README.md) - Complete guide
- [Dev Chat Widget](../dev-chat.md) - Test while developing
- [HTMX Architecture](../htmx-architecture.md) - How the UI works