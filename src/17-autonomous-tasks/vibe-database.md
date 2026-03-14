# Vibe Database

Visual PostgreSQL schema browser and SQL editor.

![Vibe Database](./assets/vibe/database.png)

---

## Overview

Vibe Database provides a visual interface for exploring your bot's PostgreSQL database. View tables, relationships, run queries, and manage data.

---

## Quick Start

1. Click **Database** button in Vibe window
2. Browse tables in left panel
3. Click table to see schema
4. Run SQL queries in editor

---

## Features

### Schema Browser
- List all tables in database
- View column definitions
- See data types and constraints
- View indexes and foreign keys

### Table Viewer
- Browse table data
- Filter and sort
- Pagination controls
- Export to CSV

### SQL Editor
- Write and execute queries
- Syntax highlighting
- Query history
- Results visualization

### Relationship Viewer
- Visual foreign key relationships
- ER diagram view
- Click to navigate related tables

---

## Interface

### Left Panel - Tables List
```
📦 customers
  ├─ id (UUID, PK)
  ├─ name (VARCHAR)
  ├─ email (VARCHAR, UNIQUE)
  ├─ created_at (TIMESTAMP)
  └─ updated_at (TIMESTAMP)

📦 orders
  ├─ id (UUID, PK)
  ├─ customer_id (UUID, FK → customers)
  ├─ total (DECIMAL)
  ├─ status (VARCHAR)
  └─ created_at (TIMESTAMP)
```

### Main Panel - Table Data
| id | name | email | created_at |
|----|------|-------|------------|
| xxx | John | john@... | 2024-01-01 |
| xxx | Jane | jane@... | 2024-01-02 |

---

## SQL Query Examples

### Select All
```sql
SELECT * FROM customers;
```

### Join Tables
```sql
SELECT o.id, c.name, o.total 
FROM orders o 
JOIN customers c ON o.customer_id = c.id;
```

### Insert
```sql
INSERT INTO customers (name, email) 
VALUES ('New Customer', 'new@example.com');
```

### Update
```sql
UPDATE customers 
SET name = 'Updated Name' 
WHERE id = 'xxx';
```

### Delete
```sql
DELETE FROM customers 
WHERE id = 'xxx';
```

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+Enter` | Execute query |
| `Ctrl+S` | Save query |
| `Ctrl+L` | Clear editor |
| `Ctrl+H` | Toggle history |

---

## Configuration

### Connection Settings
The database connects using bot configuration:
- Host: PostgreSQL server
- Port: 5432
- Database: `{bot_id}_botserver`
- User: Configured in bot settings

### Query Limits
- Default: 100 rows
- Configurable: 10 - 10000 rows
- Export: Unlimited

---

## Security

- Read-only mode available
- SQL injection protection
- Query logging for audit
- Row-level access control

---

## Troubleshooting

### Connection Failed
- Check PostgreSQL is running
- Verify bot has database credentials
- Check network connectivity

### Query Error
- Check SQL syntax
- Verify table/column names
- Review error message details

### No Tables Visible
- Bot may have no tables yet
- AI hasn't generated database schema
- Try creating app first
