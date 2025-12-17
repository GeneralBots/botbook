# Examples

> **Real-World Autonomous Tasks**

---

## Example 1: Cellphone Store CRM

### The Request

> "Create a CRM for my cellphone store with customer tracking, inventory, sales, and repair status"

### Generated Application

**URL:** `/apps/cellphone-crm`

**Tables Created:**

| Table | Fields |
|-------|--------|
| `customers` | id, name, phone, email, address, notes |
| `products` | id, name, brand, model, price, cost, stock |
| `sales` | id, customer_id, product_id, quantity, total, date |
| `repairs` | id, customer_id, device, problem, status, price |

**Features:**

- Customer list with search by name or phone
- Product inventory with low stock alerts
- Sales entry linked to customer and product
- Repair status board (Kanban style)
- Daily sales summary

### Execution

```
Step 1: Create database tables .................. ✓ (15s)
Step 2: Generate customer management UI ........ ✓ (45s)
Step 3: Generate product inventory UI .......... ✓ (30s)
Step 4: Generate sales tracking UI ............. ✓ (40s)
Step 5: Generate repair status board ........... ✓ (50s)
Step 6: Add search and filters ................. ✓ (25s)

Total time: 3 minutes 25 seconds
```

---

## Example 2: Restaurant Reservations

### The Request

> "Build a reservation system for my restaurant with table management and waitlist"

### Generated Application

**URL:** `/apps/restaurant-reservations`

**Tables Created:**

| Table | Fields |
|-------|--------|
| `tables` | id, number, capacity, location, status |
| `reservations` | id, guest_name, phone, party_size, date, time, table_id, status |
| `waitlist` | id, guest_name, phone, party_size, added_at, estimated_wait |

**Features:**

- Visual table layout with availability
- Reservation calendar view
- Real-time waitlist management
- SMS notification integration (if configured)
- Daily booking summary

---

## Example 3: Property Management

### The Request

> "Create a system to manage rental properties with tenants, leases, and maintenance requests"

### Generated Application

**URL:** `/apps/property-manager`

**Tables Created:**

| Table | Fields |
|-------|--------|
| `properties` | id, address, type, bedrooms, bathrooms, rent, status |
| `tenants` | id, name, phone, email, emergency_contact |
| `leases` | id, property_id, tenant_id, start_date, end_date, rent, deposit |
| `maintenance` | id, property_id, tenant_id, issue, priority, status, assigned_to |
| `payments` | id, lease_id, amount, date, method, status |

**Features:**

- Property listing with filters
- Tenant directory with lease history
- Maintenance request tracking (priority + status)
- Payment tracking with due date alerts
- Lease expiration reminders

---

## Example 4: Gym Membership

### The Request

> "Build a gym membership system with class scheduling and attendance tracking"

### Generated Application

**URL:** `/apps/gym-manager`

**Tables Created:**

| Table | Fields |
|-------|--------|
| `members` | id, name, phone, email, plan, start_date, expiry_date |
| `classes` | id, name, instructor, day, time, capacity, room |
| `enrollments` | id, member_id, class_id, enrolled_at |
| `attendance` | id, member_id, check_in, check_out |
| `payments` | id, member_id, amount, date, plan |

**Features:**

- Member check-in/check-out
- Class schedule with enrollment
- Attendance reports
- Membership expiry alerts
- Revenue tracking

---

## Example 5: Event Planning

### The Request

> "Create an event planning tool with guest lists, vendors, and budget tracking"

### Generated Application

**URL:** `/apps/event-planner`

**Tables Created:**

| Table | Fields |
|-------|--------|
| `events` | id, name, date, venue, budget, status |
| `guests` | id, event_id, name, email, rsvp_status, dietary_needs, table |
| `vendors` | id, event_id, name, service, contact, cost, status |
| `tasks` | id, event_id, task, assignee, due_date, status |
| `expenses` | id, event_id, category, description, amount, paid |

**Features:**

- Event dashboard with countdown
- Guest list with RSVP tracking
- Vendor management
- Task checklist
- Budget vs actual spending

---

## Example 6: Medical Clinic

### The Request

> "Build a patient management system for a small clinic with appointments and medical records"

### Generated Application

**URL:** `/apps/clinic-manager`

**Tables Created:**

| Table | Fields |
|-------|--------|
| `patients` | id, name, dob, phone, email, address, insurance |
| `appointments` | id, patient_id, doctor, date, time, reason, status |
| `records` | id, patient_id, date, diagnosis, treatment, notes, doctor |
| `prescriptions` | id, record_id, medication, dosage, duration |

**Features:**

- Patient search and history
- Appointment calendar
- Medical record timeline per patient
- Prescription tracking
- Daily appointment list per doctor

---

## Example 7: Inventory for Small Business

### The Request

> "Simple inventory tracking with suppliers, purchase orders, and stock alerts"

### Generated Application

**URL:** `/apps/inventory`

**Tables Created:**

| Table | Fields |
|-------|--------|
| `products` | id, sku, name, category, quantity, min_stock, location |
| `suppliers` | id, name, contact, email, phone, address |
| `purchase_orders` | id, supplier_id, status, total, created_at |
| `order_items` | id, order_id, product_id, quantity, unit_price |
| `stock_movements` | id, product_id, type, quantity, reason, date |

**Features:**

- Product list with stock levels
- Low stock alerts dashboard
- Supplier directory
- Purchase order creation
- Stock movement history

---

## Task Complexity Guide

| Complexity | Tables | Time | Example |
|------------|--------|------|---------|
| **Simple** | 1-2 | 1-2 min | Contact list, simple tracker |
| **Medium** | 3-5 | 3-5 min | CRM, basic inventory |
| **Complex** | 6-10 | 5-10 min | Full business management |
| **Large** | 10+ | 10+ min | ERP-style systems |

---

## Tips for Good Results

### Be Specific

✅ **Good:**
> "CRM for cellphone store with customers, products, sales, and repair tracking with status workflow"

❌ **Vague:**
> "Business app"

### Mention Key Features

✅ **Good:**
> "Inventory system with low stock alerts when below 10 units"

❌ **Missing detail:**
> "Inventory system"

### Include Workflows

✅ **Good:**
> "Repair tracking with statuses: received, diagnosing, repairing, ready, delivered"

❌ **No workflow:**
> "Track repairs"

---

## See Also

- [Task Workflow](./workflow.md) - How tasks are processed
- [App Generation](./app-generation.md) - Technical details
- [Data Model](./data-model.md) - Table structure