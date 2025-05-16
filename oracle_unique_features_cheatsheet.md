
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

---

## 📦 Oracle Built-in Packages

Oracle provides many built-in PL/SQL packages that expose powerful functionality through procedural APIs.

### 🔧 General Utility Packages

| Package          | Purpose                                      | Example                                       |
|------------------|----------------------------------------------|-----------------------------------------------|
| `DBMS_OUTPUT`    | Debug output in SQL Developer/APEX           | `DBMS_OUTPUT.PUT_LINE('Hello');`              |
| `UTL_FILE`       | Read/write files on server                   | `UTL_FILE.PUT_LINE(file, 'data');`            |
| `UTL_MAIL`       | Send emails via PL/SQL                       | `UTL_MAIL.SEND(...)`                          |
| `UTL_HTTP`       | Make HTTP requests                           | `UTL_HTTP.REQUEST('http://api.com')`          |
| `DBMS_SQL`       | Execute dynamic SQL                          | `DBMS_SQL.PARSE(...);`                        |
| `DBMS_SCHEDULER` | Schedule jobs/scripts                         | `DBMS_SCHEDULER.CREATE_JOB(...)`              |

### 📦 APEX-Specific Packages

| Package             | Purpose                                      | Example                                               |
|---------------------|----------------------------------------------|--------------------------------------------------------|
| `APEX_UTIL`         | Session/item state, user roles               | `APEX_UTIL.SET_SESSION_STATE('P1_ITEM', 'value');`     |
| `APEX_APPLICATION`  | Access app-level data                        | `APEX_APPLICATION.G_FLOW_STEP_ID`                     |
| `APEX_MAIL`         | Send emails from APEX                        | `APEX_MAIL.SEND(...)`                                 |
| `APEX_COLLECTION`   | In-memory collections                        | `APEX_COLLECTION.CREATE_COLLECTION(...)`              |
| `APEX_ITEM`         | Generate HTML form items dynamically         | `APEX_ITEM.TEXT(...)`                                 |

### 🔐 Security & Access Packages

| Package          | Purpose                                  | Example                                    |
|------------------|-------------------------------------------|--------------------------------------------|
| `DBMS_SESSION`   | Manage session attributes                 | `DBMS_SESSION.SET_IDENTIFIER('user123')`   |
| `DBMS_CRYPTO`    | Encrypt/decrypt                           | `DBMS_CRYPTO.ENCRYPT(...)`                 |
| `DBMS_RLS`       | Row-level security                        | `DBMS_RLS.ADD_POLICY(...)`                 |

---

*These packages allow developers to build secure, scalable, and automated systems inside Oracle databases and APEX apps.*

---

## 📦 Oracle Packages (Oracle-Specific Feature)

Oracle Packages are a powerful, **Oracle-exclusive** feature of PL/SQL that allow developers to group related procedures, functions, variables, constants, cursors, and exceptions into a **modular unit**.

### 🧱 Why Use Packages?

| Feature             | Description |
|---------------------|-------------|
| **Modularity**      | Group related logic (e.g., utility functions) into a single unit. |
| **Encapsulation**   | Hide implementation details; expose only what's needed via the specification. |
| **Reusability**     | Call package contents from anywhere in your application. |
| **Performance**     | Loaded once into memory — faster than standalone procedures/functions. |
| **Security**        | You can grant access at the package level rather than item by item. |

### 🧰 Package Structure

A package has two parts:

1. **Specification** – Public interface (what other code can see and call).
2. **Body** – Private logic (actual implementation).

### ✍️ Example

#### 🔹 Specification
```sql
CREATE OR REPLACE PACKAGE my_utils AS
  FUNCTION get_username(p_user_id NUMBER) RETURN VARCHAR2;
  PROCEDURE log_action(p_action VARCHAR2);
END my_utils;
```

#### 🔹 Body
```sql
CREATE OR REPLACE PACKAGE BODY my_utils AS

  FUNCTION get_username(p_user_id NUMBER) RETURN VARCHAR2 IS
    v_name VARCHAR2(100);
  BEGIN
    SELECT username INTO v_name FROM users WHERE user_id = p_user_id;
    RETURN v_name;
  END;

  PROCEDURE log_action(p_action VARCHAR2) IS
  BEGIN
    INSERT INTO action_log (action, logged_at) VALUES (p_action, SYSDATE);
  END;

END my_utils;
```

### ▶️ How to Call

```sql
-- In SQL:
SELECT my_utils.get_username(101) FROM dual;

-- In PL/SQL:
BEGIN
  my_utils.log_action('User login');
END;
```

### ❗ Oracle-Only Feature

| Feature                     | Oracle | PostgreSQL/MySQL/SQL Server |
|-----------------------------|--------|------------------------------|
| Grouped procedures/functions in one unit | ✅ Yes | ❌ No |
| Public/private scoping within a DB object | ✅ Yes | ❌ No |
| Memory-loaded modules for performance | ✅ Yes | ❌ No |
| Function/procedure overloading in a package | ✅ Yes | ❌ No |

*Packages are one of Oracle PL/SQL's most powerful and unique offerings. No direct equivalent exists in MySQL, PostgreSQL, or SQL Server.*

