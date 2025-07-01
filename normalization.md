# 📘 Database Normalization to 3NF

## 🎯 Objective

To ensure our database schema is clean, efficient, and free from redundancy by applying the principles of normalization up to the Third Normal Form (3NF).

---

## 🔍 What is Normalization?

Normalization is the process of organizing data in a database to:
- Reduce redundancy
- Improve data integrity
- Ensure data dependencies make sense

We apply normalization in steps called "normal forms": 1NF → 2NF → 3NF.

---

## ✅ Step-by-Step Normalization

### 1️⃣ First Normal Form (1NF)

**Rule:**  
- Ensure each table column contains atomic (indivisible) values.
- No repeating groups or arrays.

**✅ Applied:**  
All attributes in our schema are atomic. For example:
- `first_name`, `email`, and `pricepernight` contain single values only.
- There are no repeating fields or multi-valued attributes.

---

### 2️⃣ Second Normal Form (2NF)

**Rule:**  
- Must be in 1NF.
- All non-key attributes must be fully functionally dependent on the whole primary key.

**✅ Applied:**  
- We use UUIDs as primary keys for each table, which are not composite.
- Each non-key attribute depends entirely on the primary key of its table.
- No partial dependencies exist.

---

### 3️⃣ Third Normal Form (3NF)

**Rule:**  
- Must be in 2NF.
- There should be no transitive dependency (i.e., non-key attribute depending on another non-key attribute).

**✅ Applied:**  
- All non-key attributes directly depend on the primary key and not on other non-key attributes.
- For example, in the `Booking` table, `status`, `total_price`, and `start_date` all depend directly on `booking_id`.

---

## 🧠 Optional Consideration: Location Normalization

In the `Property` table:
```sql
location: VARCHAR ```

If many properties share the same city or area, it may be beneficial to normalize location into a separate table to reduce redundancy.

Example:

`Location` Table:

```sql
location_id (PK), city, state, country```

`Property` Table (updated):

```sql
location_id (FK → Location)```

This normalization is optional, based on how often location data is reused or queried by subfields.
