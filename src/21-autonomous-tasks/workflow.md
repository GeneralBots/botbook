# Task Workflow

> **From Intent to Working Application**

---

## The Four Phases

Every autonomous task goes through four phases:

```
DESCRIBE → PLAN → EXECUTE → DELIVER
```

---

## Phase 1: Describe

You describe what you want in plain language:

> "Create a CRM for my cellphone store"

The system extracts:

| Element | Extracted Value |
|---------|-----------------|
| **Action** | Create application |
| **Type** | CRM |
| **Domain** | Cellphone retail |
| **Implied entities** | customers, products, sales |

### Good Descriptions

| ✅ Good | ❌ Too Vague |
|---------|--------------|
| "CRM for cellphone store with customer tracking and repair status" | "Make an app" |
| "Sales dashboard showing daily revenue and top products" | "Dashboard" |
| "Inventory system with stock alerts when below 10 units" | "Track stuff" |

### Adding Context

Be specific about your needs:

```
"Create a CRM for my cellphone store with:
- Customer list with name, phone, email
- Product inventory with brand, model, price, stock
- Sales tracking linked to customers and products
- Repair status board (received, diagnosing, repairing, ready, delivered)
- Search by customer name or phone number"
```

---

## Phase 2: Plan

The system creates an execution plan:

```
┌────────────────────────────────────────────────────────────────┐
│ TASK: Cellphone Store CRM                                       │
│ Confidence: 92% | Risk: Low | ETA: 5 minutes                   │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│ Step 1: Create database tables              [CRITICAL]         │
│         → customers, products, sales, repairs                   │
│                                                                 │
│ Step 2: Generate application UI             [HIGH]             │
│         → List views, forms, navigation                        │
│                                                                 │
│ Step 3: Add search and filters              [MEDIUM]           │
│         → Name search, status filters                          │
│                                                                 │
│ Step 4: Configure repair workflow           [MEDIUM]           │
│         → Status transitions, notifications                    │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
```

### Plan Review

Before execution, you can:

- **Accept** - Proceed with the plan
- **Modify** - Adjust steps or requirements
- **Cancel** - Discard and start over

### Step Priorities

| Priority | Meaning |
|----------|---------|
| **CRITICAL** | Must succeed for app to work |
| **HIGH** | Core functionality |
| **MEDIUM** | Important features |
| **LOW** | Nice to have |

---

## Phase 3: Execute

The system executes each step:

```
[████████████████████░░░░░░░░░░] 65%

Step 2 of 4: Generate application UI
├─ Creating customer list view... ✓
├─ Creating product list view... ✓
├─ Creating sales form...
└─ Remaining: repair board, navigation

ETA: 2 minutes
```

### Execution Modes

| Mode | Behavior | Best For |
|------|----------|----------|
| **Automatic** | Runs all steps without stopping | Trusted, simple tasks |
| **Supervised** | Pauses before each step | Learning, complex tasks |
| **Dry Run** | Shows what would happen | Testing, verification |

### Pause and Resume

Tasks can be paused at any time:

```
[PAUSED] Step 2 of 4: Generate application UI

Progress saved. Resume anytime with:
  → Click "Resume" in Tasks
  → Say "continue my CRM task"
```

When you resume, execution continues from exactly where it stopped.

---

## Phase 4: Deliver

When complete, you receive:

```
┌────────────────────────────────────────────────────────────────┐
│ ✅ TASK COMPLETE                                                │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│ Application: Cellphone Store CRM                               │
│ URL: /apps/cellphone-crm                                       │
│                                                                 │
│ Created:                                                        │
│   📋 4 database tables (customers, products, sales, repairs)   │
│   📱 5 views (lists + forms)                                   │
│   🔍 Search by name, phone, status                             │
│   📊 Repair status workflow                                    │
│                                                                 │
│ [Open App]  [View Details]  [Create Another]                   │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
```

---

## Stored Steps

Every step is stored in the database:

```sql
-- task_steps table
task_id     | step_order | name                    | status    | progress
------------|------------|-------------------------|-----------|----------
abc123      | 1          | Create database tables  | completed | 100
abc123      | 2          | Generate application UI | completed | 100
abc123      | 3          | Add search and filters  | completed | 100
abc123      | 4          | Configure repair flow   | completed | 100
```

### Why Store Steps?

1. **Resume interrupted tasks** - Power outage? Network issue? Just continue.
2. **Track progress** - Know exactly where a task is
3. **Debug failures** - See which step failed and why
4. **Audit trail** - Record of what was done

---

## Error Handling

When a step fails:

```
[ERROR] Step 3: Add search and filters

Error: Could not create full-text index on 'customers' table
Reason: Column 'notes' exceeds maximum indexable length

Options:
  [Retry]     - Try the step again
  [Skip]      - Continue without this feature
  [Modify]    - Change the approach
  [Cancel]    - Stop the task
```

### Automatic Recovery

For transient errors (network timeouts, temporary unavailability), the system automatically retries up to 3 times with exponential backoff.

---

## Approvals

High-impact steps may require approval:

```
┌────────────────────────────────────────────────────────────────┐
│ ⚠️ APPROVAL REQUIRED                                           │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│ Step: Create database tables                                   │
│                                                                 │
│ This will create 4 new tables:                                 │
│   • customers (6 columns)                                      │
│   • products (7 columns)                                       │
│   • sales (5 columns)                                          │
│   • repairs (8 columns)                                        │
│                                                                 │
│ Impact: Database storage increase ~1MB                         │
│                                                                 │
│ [Approve]  [Modify]  [Reject]                                  │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
```

### What Requires Approval?

| Action | Default |
|--------|---------|
| Create tables | Auto-approve |
| Delete data | Requires approval |
| External API calls | Configurable |
| Email sending | Requires approval |
| File deletion | Requires approval |

---

## Task States

```
                    ┌─────────────┐
                    │   DRAFT     │ Task created, not started
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  PLANNING   │ Generating execution plan
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │   READY     │ Plan complete, awaiting start
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
       ┌──────▼──────┐ ┌───▼───┐ ┌─────▼─────┐
       │   RUNNING   │ │PAUSED │ │ APPROVAL  │
       └──────┬──────┘ └───┬───┘ │  PENDING  │
              │            │     └─────┬─────┘
              │            │           │
              └────────────┼───────────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
       ┌──────▼──────┐ ┌───▼───┐ ┌─────▼─────┐
       │  COMPLETED  │ │FAILED │ │ CANCELLED │
       └─────────────┘ └───────┘ └───────────┘
```

---

## See Also

- [App Generation](./app-generation.md) - How apps are built
- [Progress Tracking](./progress.md) - Monitoring your tasks
- [Examples](./examples.md) - Real-world workflows