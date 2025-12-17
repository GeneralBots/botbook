# Data Model

> **Tables Created for Your Application**

---

## Overview

When you create an autonomous task that generates an application, the system automatically creates the database tables needed to store your data. These tables are real PostgreSQL tables with proper types, indexes, and relationships.

---

## The user_data System

Under the hood, all application data is managed through the `user_data` virtual table system. This provides:

- **Namespacing** - Each app's tables are isolated
- **Multi-tenancy** - Your data is separate from other users
- **Flexibility** - Tables can be created dynamically
- **Security** - Access control per table

### How It Works

Apps run inside botui (Suite), which proxies all API calls to botserver. The app context flows automatically:

```
┌─────────────────────────────────────────────────────────────┐
│  botui (Suite)                                              │
│                                                             │
│  ┌───────────────────────────────────────────────────────┐ │
│  │  Your App: /apps/cellphone-crm/                       │ │
│  │                                                       │ │
│  │  <form hx-post="/api/db/customers">                  │ │
│  │                                                       │ │
│  └───────────────────────────────────────────────────────┘ │
│                         │                                   │
│                         ▼                                   │
│  ┌───────────────────────────────────────────────────────┐ │
│  │  botui proxy                                          │ │
│  │  - Adds X-App-Context: cellphone-crm                 │ │
│  │  - Forwards to botserver                             │ │
│  └───────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│  botserver                                                  │
│                                                             │
│  POST /api/db/customers                                    │
│  X-App-Context: cellphone-crm                              │
│                         │                                   │
│                         ▼                                   │
│  Routes to: user_data WHERE app='cellphone-crm'            │
│                         AND table='customers'               │
└─────────────────────────────────────────────────────────────┘
```

### App Context Detection

botui proxy determines the app from the request URL and injects the `X-App-Context` header:

| Request From | App Context |
|--------------|-------------|
| `/apps/cellphone-crm/*` | `cellphone-crm` |
| `/apps/inventory/*` | `inventory` |
| Suite main (no app) | `default` |

### Generated HTMX (No Special Headers Needed)

```html
<!-- Your app just uses normal HTMX -->
<form hx-post="/api/db/customers">
    <input name="name">
    <button>Add</button>
</form>

<!-- botui proxy automatically adds X-App-Context -->
```

### For External API Clients

```bash
# Must include X-App-Context header
curl -X POST https://bot.example.com/api/db/customers \
  -H "X-App-Context: cellphone-crm" \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"name": "John"}'
```

---

## Table Creation

When you describe your app, the system infers the tables needed:

**Your description:**
> "CRM for cellphone store with customer tracking, sales, and repairs"

**Tables created:**

| Table | Purpose |
|-------|---------|
| `customers` | Customer records |
| `products` | Inventory items |
| `sales` | Transaction records |
| `repairs` | Service tickets |

---

## Generated Schema

### customers

```sql
CREATE TABLE customers (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name        TEXT NOT NULL,
    phone       TEXT,
    email       TEXT,
    address     TEXT,
    notes       TEXT,
    created_at  TIMESTAMPTZ DEFAULT NOW(),
    updated_at  TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX idx_customers_name ON customers USING gin(name gin_trgm_ops);
CREATE INDEX idx_customers_phone ON customers(phone);
```

### products

```sql
CREATE TABLE products (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name        TEXT NOT NULL,
    brand       TEXT,
    model       TEXT,
    price       DECIMAL(10,2),
    cost        DECIMAL(10,2),
    stock       INTEGER DEFAULT 0,
    min_stock   INTEGER DEFAULT 5,
    category    TEXT,
    created_at  TIMESTAMPTZ DEFAULT NOW(),
    updated_at  TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX idx_products_brand ON products(brand);
CREATE INDEX idx_products_category ON products(category);
```

### sales

```sql
CREATE TABLE sales (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    customer_id UUID REFERENCES customers(id),
    product_id  UUID REFERENCES products(id),
    quantity    INTEGER NOT NULL DEFAULT 1,
    unit_price  DECIMAL(10,2),
    total       DECIMAL(10,2),
    payment     TEXT,
    notes       TEXT,
    created_at  TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX idx_sales_customer ON sales(customer_id);
CREATE INDEX idx_sales_date ON sales(created_at);
```

### repairs

```sql
CREATE TABLE repairs (
    id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    customer_id UUID REFERENCES customers(id),
    device      TEXT NOT NULL,
    brand       TEXT,
    model       TEXT,
    problem     TEXT,
    diagnosis   TEXT,
    solution    TEXT,
    status      TEXT DEFAULT 'received',
    price       DECIMAL(10,2),
    received_at TIMESTAMPTZ DEFAULT NOW(),
    completed_at TIMESTAMPTZ,
    created_at  TIMESTAMPTZ DEFAULT NOW(),
    updated_at  TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX idx_repairs_customer ON repairs(customer_id);
CREATE INDEX idx_repairs_status ON repairs(status);
```

---

## Data Types

The system automatically selects appropriate types:

| Field Pattern | SQL Type | Example |
|---------------|----------|---------|
| `name`, `title`, `description` | TEXT | Customer name |
| `email` | TEXT (validated) | john@example.com |
| `phone` | TEXT | +1-555-0123 |
| `price`, `cost`, `amount`, `total` | DECIMAL(10,2) | 299.99 |
| `quantity`, `stock`, `count` | INTEGER | 10 |
| `date`, `_at` suffix | TIMESTAMPTZ | 2024-01-15T10:30:00Z |
| `is_`, `has_` prefix | BOOLEAN | true |
| `id` | UUID | a1b2c3d4-... |
| `_id` suffix | UUID (FK) | References another table |

---

## Relationships

Foreign keys are created automatically when fields end with `_id`:

```
customers
    │
    ├──< sales (customer_id → customers.id)
    │
    └──< repairs (customer_id → customers.id)

products
    │
    └──< sales (product_id → products.id)
```

---

## Accessing Data

### From Your App (HTMX)

```html
<!-- List all customers -->
<div hx-get="/api/db/customers" hx-trigger="load">

<!-- Get one customer -->
<div hx-get="/api/db/customers/abc123">

<!-- Create customer -->
<form hx-post="/api/db/customers">

<!-- Update customer -->
<form hx-put="/api/db/customers/abc123">

<!-- Delete customer -->
<button hx-delete="/api/db/customers/abc123">
```

### From Chat

> "Show me all customers who bought an iPhone"

The bot queries the database and responds with results.

### API Response Format

```json
{
    "data": [
        {
            "id": "abc123",
            "name": "John Smith",
            "phone": "+1-555-0123",
            "email": "john@example.com",
            "created_at": "2024-01-15T10:30:00Z"
        }
    ],
    "total": 150,
    "limit": 20,
    "offset": 0
}
```

---

## Filtering and Querying

### Simple Filters

```
GET /api/db/repairs?status=ready
GET /api/db/products?brand=Apple
GET /api/db/sales?customer_id=abc123
```

### Search

```
GET /api/db/customers?q=john
```

Searches across all text fields.

### Sorting

```
GET /api/db/sales?sort=created_at&order=desc
```

### Pagination

```
GET /api/db/customers?limit=20&offset=40
```

### Comparison Operators

```
GET /api/db/products?price_gt=100        # Greater than
GET /api/db/products?stock_lt=5          # Less than
GET /api/db/products?stock_gte=10        # Greater or equal
GET /api/db/repairs?status_ne=completed  # Not equal
```

---

## Schema Storage

Table definitions are stored in `schema.json`:

```json
{
    "app": "cellphone-crm",
    "tables": {
        "customers": {
            "columns": {
                "id": {"type": "uuid", "primary": true},
                "name": {"type": "text", "required": true},
                "phone": {"type": "text"},
                "email": {"type": "text"}
            },
            "indexes": ["name", "phone"]
        },
        "products": {
            "columns": {
                "id": {"type": "uuid", "primary": true},
                "name": {"type": "text", "required": true},
                "price": {"type": "decimal"},
                "stock": {"type": "integer", "default": 0}
            }
        }
    },
    "relationships": [
        {"from": "sales.customer_id", "to": "customers.id"},
        {"from": "sales.product_id", "to": "products.id"},
        {"from": "repairs.customer_id", "to": "customers.id"}
    ]
}
```

---

## Adding Tables Later

You can ask to add tables to an existing app:

> "Add a suppliers table to my cellphone CRM"

The system will:
1. Create the `suppliers` table
2. Update `schema.json`
3. Add UI elements if requested

---

## Data Import

Import existing data via:

### CSV Upload

```
Upload suppliers.csv to /apps/cellphone-crm/import
```

### API

```bash
curl -X POST /api/db/customers/import \
  -H "Content-Type: text/csv" \
  --data-binary @customers.csv
```

### Chat

> "Import customers from the Excel file I uploaded"

---

## See Also

- [App Generation](./app-generation.md) - How apps are created
- [REST API](../10-rest/README.md) - Full API reference
- [Storage API](../10-rest/storage-api.md) - File storage