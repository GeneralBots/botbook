# App Generation

> **HTMX Applications Connected to botserver**

---

## Overview

When you request an application, the system generates a complete HTMX frontend that communicates directly with botserver's API. No middleware, no separate backend - just HTML that talks to the API.

---

## The Generated Stack

```
┌─────────────────────────────────────────────────────────────────┐
│                    Generated Application                         │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    index.html                            │   │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐   │   │
│  │  │  Lists  │  │  Forms  │  │ Actions │  │ Filters │   │   │
│  │  └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘   │   │
│  │       └───────────┬┴───────────┴┬───────────┘         │   │
│  │                   │   HTMX      │                      │   │
│  └───────────────────┼─────────────┼──────────────────────┘   │
└──────────────────────┼─────────────┼──────────────────────────┘
                       │             │
                       ▼             ▼
┌─────────────────────────────────────────────────────────────────┐
│                       botserver API                              │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐                │
│  │ /api/db/*  │  │/api/drive/*│  │ /api/llm/* │                │
│  │   CRUD     │  │   Files    │  │     AI     │                │
│  └─────┬──────┘  └─────┬──────┘  └─────┬──────┘                │
│        └───────────────┼───────────────┘                        │
│                        ▼                                         │
│              PostgreSQL + MinIO                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Generated File Structure

When you create an app called "cellphone-crm", this is created:

```
.gbdrive/apps/cellphone-crm/
├── index.html              # Main application
├── _assets/
│   ├── htmx.min.js         # HTMX library
│   ├── app.js              # App-specific JavaScript
│   └── styles.css          # Styling
└── schema.json             # Table definitions
```

---

## HTMX Patterns Used

### List View with Auto-Refresh

```html
<div id="customers"
     hx-get="/api/db/customers"
     hx-trigger="load, every 30s"
     hx-swap="innerHTML">
    Loading customers...
</div>
```

### Create Form

```html
<form hx-post="/api/db/customers"
      hx-target="#customers"
      hx-swap="afterbegin"
      hx-indicator=".loading">
    
    <input name="name" placeholder="Customer name" required>
    <input name="phone" type="tel" placeholder="Phone">
    <input name="email" type="email" placeholder="Email">
    
    <button type="submit">
        Add Customer
        <span class="loading htmx-indicator">...</span>
    </button>
</form>
```

### Edit in Place

```html
<tr hx-get="/api/db/customers/${id}/edit"
    hx-trigger="dblclick"
    hx-swap="outerHTML">
    <td>${name}</td>
    <td>${phone}</td>
    <td>${email}</td>
</tr>
```

### Delete with Confirmation

```html
<button hx-delete="/api/db/customers/${id}"
        hx-target="closest tr"
        hx-swap="outerHTML swap:0.5s"
        hx-confirm="Delete this customer?">
    🗑️
</button>
```

### Search

```html
<input type="search"
       name="q"
       placeholder="Search customers..."
       hx-get="/api/db/customers"
       hx-trigger="keyup changed delay:300ms"
       hx-target="#customers">
```

### Filter Dropdown

```html
<select name="status"
        hx-get="/api/db/repairs"
        hx-trigger="change"
        hx-target="#repairs">
    <option value="">All Status</option>
    <option value="received">Received</option>
    <option value="repairing">Repairing</option>
    <option value="ready">Ready</option>
</select>
```

---

## API Endpoints Your App Uses

### App Context is Automatic

Your app runs inside botui (Suite). The botui proxy automatically:

1. Detects your app from the URL (`/apps/cellphone-crm/`)
2. Injects `X-App-Context: cellphone-crm` header
3. Forwards to botserver

**You don't need to do anything special** - just use normal HTMX:

```html
<!-- botui handles the app context automatically -->
<form hx-post="/api/db/customers">
    <input name="name">
    <button>Add</button>
</form>
```

### Endpoints

| HTMX Call | Endpoint | What It Does |
|-----------|----------|--------------|
| `hx-get="/api/db/customers"` | GET | List all customers |
| `hx-get="/api/db/customers?q=john"` | GET | Search customers |
| `hx-post="/api/db/customers"` | POST | Create customer |
| `hx-put="/api/db/customers/123"` | PUT | Update customer |
| `hx-delete="/api/db/customers/123"` | DELETE | Delete customer |

### Query Parameters

| Parameter | Example | Purpose |
|-----------|---------|---------|
| `q` | `?q=john` | Full-text search |
| `sort` | `?sort=created_at` | Sort field |
| `order` | `?order=desc` | Sort direction |
| `limit` | `?limit=20` | Results per page |
| `offset` | `?offset=40` | Pagination |
| `{field}` | `?status=active` | Filter by field |

---

## Example: Cellphone CRM

For a cellphone store CRM, the generated app includes:

### Customer List

```html
<section id="customers-section">
    <header>
        <h2>Customers</h2>
        <input type="search" 
               hx-get="/api/db/customers"
               hx-trigger="keyup changed delay:300ms"
               hx-target="#customer-list"
               placeholder="Search by name or phone...">
        <button onclick="openModal('add-customer')">+ Add Customer</button>
    </header>
    
    <table>
        <thead>
            <tr>
                <th>Name</th>
                <th>Phone</th>
                <th>Email</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody id="customer-list"
               hx-get="/api/db/customers"
               hx-trigger="load">
        </tbody>
    </table>
</section>
```

### Sales Form

```html
<form id="new-sale"
      hx-post="/api/db/sales"
      hx-target="#recent-sales"
      hx-swap="afterbegin">
    
    <select name="customer_id" required
            hx-get="/api/db/customers"
            hx-trigger="load"
            hx-target="this"
            hx-swap="innerHTML">
        <option>Loading customers...</option>
    </select>
    
    <select name="product_id" required
            hx-get="/api/db/products?stock_gt=0"
            hx-trigger="load"
            hx-target="this"
            hx-swap="innerHTML">
        <option>Loading products...</option>
    </select>
    
    <input name="quantity" type="number" min="1" value="1">
    
    <button type="submit">Complete Sale</button>
</form>
```

### Repair Status Board

```html
<div class="kanban-board">
    <div class="column" data-status="received">
        <h3>Received</h3>
        <div hx-get="/api/db/repairs?status=received"
             hx-trigger="load, every 60s">
        </div>
    </div>
    
    <div class="column" data-status="diagnosing">
        <h3>Diagnosing</h3>
        <div hx-get="/api/db/repairs?status=diagnosing"
             hx-trigger="load, every 60s">
        </div>
    </div>
    
    <div class="column" data-status="repairing">
        <h3>Repairing</h3>
        <div hx-get="/api/db/repairs?status=repairing"
             hx-trigger="load, every 60s">
        </div>
    </div>
    
    <div class="column" data-status="ready">
        <h3>Ready for Pickup</h3>
        <div hx-get="/api/db/repairs?status=ready"
             hx-trigger="load, every 60s">
        </div>
    </div>
</div>
```

---

## Styling

Generated apps use CSS custom properties for easy theming:

```css
:root {
    --primary: #0ea5e9;
    --success: #22c55e;
    --warning: #f59e0b;
    --danger: #ef4444;
    --bg: #ffffff;
    --text: #1e293b;
    --border: #e2e8f0;
    --radius: 8px;
}

/* Dark mode automatic */
@media (prefers-color-scheme: dark) {
    :root {
        --bg: #0f172a;
        --text: #f1f5f9;
        --border: #334155;
    }
}
```

---

## JavaScript Helpers

`app.js` includes utilities for common operations:

```javascript
// Toast notifications
function toast(message, type = 'info') {
    // Shows a temporary notification
}

// Modal management
function openModal(id) { ... }
function closeModal(id) { ... }

// HTMX event handling
document.body.addEventListener('htmx:afterSwap', (e) => {
    // Update UI after data changes
});

document.body.addEventListener('htmx:responseError', (e) => {
    toast('Error: ' + e.detail.error, 'error');
});
```

---

## Bot Integration

Your generated app can talk to the bot for AI features:

```html
<!-- AI-assisted customer lookup -->
<form hx-post="/api/llm/complete"
      hx-target="#ai-result">
    <input name="prompt" 
           placeholder="Find customers who bought iPhones last month">
    <button type="submit">🤖 Ask AI</button>
</form>

<!-- AI generates the query, executes it, returns results -->
<div id="ai-result"></div>
```

---

## Customization After Generation

Generated apps can be modified:

1. **Edit directly** - Modify `index.html` in `.gbdrive/apps/`
2. **Use Designer** - Visual editor in Suite
3. **Regenerate** - Ask for changes, system updates the app

---

## See Also

- [Data Model](./data-model.md) - How tables are created
- [Progress Tracking](./progress.md) - Monitor generation
- [HTMX Architecture](../04-gbui/htmx-architecture.md) - Frontend patterns
- [REST API](../10-rest/README.md) - API reference