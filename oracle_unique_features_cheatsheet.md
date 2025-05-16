
# Unique Oracle SQL & PL/SQL Features Cheat Sheet

This document covers powerful features unique to Oracle that are useful in both APEX and general database development.

---

## 🧱 PL/SQL Blocks

Oracle's procedural extension to SQL. Used in triggers, dynamic actions, and stored logic.

```sql
DECLARE
  v_name VARCHAR2(50);
BEGIN
  SELECT name INTO v_name FROM employees WHERE id = 101;
  DBMS_OUTPUT.PUT_LINE(v_name);
END;
```

---

## 📄 Dual Table

A one-row, one-column table useful for testing expressions.

```sql
SELECT SYSDATE FROM dual;
SELECT 1 + 1 FROM dual;
```

---

## 🔁 Sequences

Oracle's way to auto-generate unique IDs.

```sql
CREATE SEQUENCE emp_seq START WITH 1000 INCREMENT BY 1;
SELECT emp_seq.NEXTVAL FROM dual;
```

---

## 🔢 ROWNUM and ROWID

- `ROWNUM`: Row numbering for filtering.
- `ROWID`: Unique physical row address.

```sql
SELECT * FROM employees WHERE ROWNUM <= 5;
```

---

## 🔄 MERGE Statement (UPSERT)

Efficient insert/update operation.

```sql
MERGE INTO employees e
USING temp_employees t
ON (e.id = t.id)
WHEN MATCHED THEN
  UPDATE SET e.salary = t.salary
WHEN NOT MATCHED THEN
  INSERT (id, name, salary) VALUES (t.id, t.name, t.salary);
```

---

## 🧠 %TYPE and %ROWTYPE

Dynamic typing based on table structure.

```sql
v_salary employees.salary%TYPE;
emp_record employees%ROWTYPE;
```

---

## ⚠️ Exception Handling

Handle errors with custom logic.

```sql
BEGIN
  -- code
EXCEPTION
  WHEN NO_DATA_FOUND THEN
    DBMS_OUTPUT.PUT_LINE('Not found');
  WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE(SQLERRM);
END;
```

---

## 🧾 Autonomous Transactions

Allows a procedure to commit independently.

```sql
PRAGMA AUTONOMOUS_TRANSACTION;
```

---

## 🔗 APEX Bind Variables

Reference APEX page items.

```sql
:P1_USER_ID
```

---

## ⏱ DBMS_SCHEDULER

Schedule jobs in the background.

```sql
DBMS_SCHEDULER.CREATE_JOB(...);
```

---

## 🧮 Virtual Columns

Define computed columns in a table.

```sql
full_name AS (first_name || ' ' || last_name)
```

---

## 🕒 Flashback Queries

Query data as it existed in the past.

```sql
SELECT * FROM employees AS OF TIMESTAMP (SYSTIMESTAMP - INTERVAL '5' MINUTE);
```

---

## 📦 User-Defined Types (UDTs)

Create structured data types.

```sql
CREATE TYPE address_type AS OBJECT (
  street VARCHAR2(100),
  city   VARCHAR2(50)
);
```

---

## 📚 PL/SQL Collections

Oracle arrays and tables.

```sql
TYPE id_array IS TABLE OF NUMBER INDEX BY BINARY_INTEGER;
```

---

## 🧠 Materialized Views

Stored and refreshable result sets.

```sql
CREATE MATERIALIZED VIEW mv_employees REFRESH FAST AS
SELECT * FROM employees;
```

---

## ⚙️ Optional Advanced Features

- Context variables: `USER`, `SYSDATE`, `CURRENT_SCHEMA`
- `DBMS_METADATA`: Get DDL for any object
- Invisible columns
- Partitioning
- Edition-based redefinition

---

*This file is intended as a plug-in cheat sheet for developers using Oracle-specific features in APEX, PL/SQL, or enterprise applications.*
