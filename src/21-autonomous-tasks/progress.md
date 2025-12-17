# Progress Tracking

> **Know Where Your Task Is**

---

## Overview

Every autonomous task shows real-time progress so you always know:

- What step is running
- How far along it is
- How much time remains
- If anything needs your attention

---

## The Progress View

```
┌────────────────────────────────────────────────────────────────┐
│ Cellphone Store CRM                                            │
│                                                                 │
│ [████████████████████░░░░░░░░░░] 65%                           │
│                                                                 │
│ Step 2 of 4: Generate application UI                           │
│ ├─ Customer list view ✓                                        │
│ ├─ Product list view ✓                                         │
│ ├─ Sales form ◐ (in progress)                                  │
│ └─ Repair board ○ (pending)                                    │
│                                                                 │
│ Started: 2 min ago                                              │
│ ETA: 3 min remaining                                            │
│                                                                 │
│ [Pause]  [Cancel]                                               │
└────────────────────────────────────────────────────────────────┘
```

---

## Progress Indicators

| Symbol | Meaning |
|--------|---------|
| ✓ | Completed |
| ◐ | In progress |
| ○ | Pending |
| ⚠ | Needs attention |
| ✕ | Failed |
| ⏸ | Paused |

---

## Step States

Each step goes through these states:

```
pending → running → completed
                  ↘ failed
                  ↘ skipped
```

### State Details

| State | Description | Action |
|-------|-------------|--------|
| `pending` | Waiting to start | None needed |
| `running` | Currently executing | Monitor progress |
| `completed` | Successfully finished | None needed |
| `failed` | Encountered error | Review and retry/skip |
| `skipped` | Intentionally bypassed | None needed |
| `paused` | Waiting for resume | Click Resume |
| `approval` | Needs your approval | Approve or reject |

---

## Real-Time Updates

Progress updates via WebSocket:

```javascript
// Connect to task updates
const ws = new WebSocket('/ws/tasks');

ws.onmessage = (event) => {
    const update = JSON.parse(event.data);
    
    switch (update.type) {
        case 'progress':
            // Update progress bar
            updateProgress(update.percent);
            break;
            
        case 'step_complete':
            // Mark step as done
            markStepComplete(update.step);
            break;
            
        case 'approval_needed':
            // Show approval dialog
            showApproval(update.approval);
            break;
            
        case 'task_complete':
            // Show completion
            showComplete(update.result);
            break;
    }
};
```

---

## Stored Progress

Progress is persisted to the database so you can:

### Resume After Interruption

If you close your browser or lose connection:

1. Task continues running on the server
2. When you return, progress is restored
3. You see exactly where it is

### Continue Later

If you pause a task:

1. Current state is saved
2. Come back anytime
3. Click Resume to continue from the exact point

### Review History

```sql
-- task_progress table
task_id   | step    | percent | status    | updated_at
----------|---------|---------|-----------|--------------------
abc123    | 1       | 100     | completed | 2024-01-15 10:00:15
abc123    | 2       | 65      | running   | 2024-01-15 10:02:30
abc123    | 3       | 0       | pending   | NULL
abc123    | 4       | 0       | pending   | NULL
```

---

## Progress API

### Get Task Progress

```http
GET /api/tasks/{task_id}/progress
```

**Response:**

```json
{
    "task_id": "abc123",
    "title": "Cellphone Store CRM",
    "status": "running",
    "progress": 65,
    "current_step": 2,
    "total_steps": 4,
    "started_at": "2024-01-15T10:00:00Z",
    "eta_seconds": 180,
    "steps": [
        {
            "order": 1,
            "name": "Create database tables",
            "status": "completed",
            "progress": 100,
            "duration_ms": 15000
        },
        {
            "order": 2,
            "name": "Generate application UI",
            "status": "running",
            "progress": 65,
            "substeps": [
                {"name": "Customer list", "done": true},
                {"name": "Product list", "done": true},
                {"name": "Sales form", "done": false},
                {"name": "Repair board", "done": false}
            ]
        },
        {
            "order": 3,
            "name": "Add search and filters",
            "status": "pending",
            "progress": 0
        },
        {
            "order": 4,
            "name": "Configure workflows",
            "status": "pending",
            "progress": 0
        }
    ]
}
```

### Subscribe to Updates

```http
WS /ws/tasks/{task_id}
```

Receives real-time progress updates.

---

## Progress in Chat

Ask your bot about task progress:

> "How's my CRM task going?"

**Bot response:**
```
📊 Your Cellphone Store CRM task is 65% complete.

Currently: Generating application UI
- ✓ Customer list view
- ✓ Product list view
- ⏳ Sales form (in progress)
- ⏳ Repair board

ETA: About 3 minutes remaining.
```

---

## Notifications

Get notified when:

| Event | Notification |
|-------|--------------|
| Task starts | "Your CRM task has started" |
| Step completes | "Step 1 complete: Database created" |
| Approval needed | "⚠️ Approval required for Step 3" |
| Task completes | "✅ Your CRM is ready!" |
| Task fails | "❌ Task failed at Step 2" |

### Notification Channels

- **Browser** - Desktop notifications
- **Email** - For long-running tasks
- **Chat** - Bot sends you updates
- **Mobile** - Push notifications (if app installed)

---

## Time Estimates

The system estimates remaining time based on:

1. **Historical data** - How long similar steps took before
2. **Current progress** - How fast the current step is moving
3. **Complexity** - More complex apps take longer

### Estimate Accuracy

| Task Complexity | Estimate Accuracy |
|-----------------|-------------------|
| Simple (1-2 tables) | ±20% |
| Medium (3-5 tables) | ±30% |
| Complex (6+ tables) | ±50% |

---

## Handling Slow Tasks

If a task is taking longer than expected:

### Check Progress

```
"Status of my CRM task"
```

### See Detailed Logs

```
"Show logs for my CRM task"
```

### Cancel and Retry

```
"Cancel my CRM task and start over"
```

---

## Progress Best Practices

### Monitor Long Tasks

For tasks over 10 minutes:
- Enable email notifications
- Check in periodically
- Have fallback plans

### Pause Before Leaving

If you need to leave:
- Pause the task
- It saves state
- Resume when ready

### Review Failed Steps

When a step fails:
1. Check the error message
2. Understand what went wrong
3. Retry, skip, or modify

---

## See Also

- [Task Workflow](./workflow.md) - The complete task flow
- [App Generation](./app-generation.md) - What gets generated
- [Examples](./examples.md) - Real task examples