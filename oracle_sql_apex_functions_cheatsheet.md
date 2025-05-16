
# Oracle SQL Functions & Packages Cheat Sheet

This cheat sheet contains commonly used SQL functions and Oracle packages, including APEX-specific tools, with examples.

---

## 🧠 SQL Functions (Built-In)

### 🔤 Character Functions

| Function    | Purpose                                 | Example                              |
|-------------|------------------------------------------|--------------------------------------|
| `UPPER()`   | Converts to uppercase                    | `UPPER('oracle') → 'ORACLE'`        |
| `LOWER()`   | Converts to lowercase                    | `LOWER('APEX') → 'apex'`            |
| `INITCAP()` | Capitalizes first letter of each word   | `INITCAP('oracle sql') → 'Oracle Sql'` |
| `SUBSTR()`  | Extracts part of a string                | `SUBSTR('Oracle', 1, 3) → 'Ora'`    |
| `LENGTH()`  | Returns string length                    | `LENGTH('Hello') → 5`               |
| `INSTR()`   | Finds position of substring              | `INSTR('hello world', 'o') → 5`     |
| `TRIM()`    | Trims characters from both ends         | `TRIM(' H ') → 'H'`                 |

### 🔢 Number Functions

| Function    | Purpose                                 | Example                               |
|-------------|------------------------------------------|---------------------------------------|
| `ROUND()`   | Rounds a number                          | `ROUND(123.456, 2) → 123.46`         |
| `TRUNC()`   | Truncates decimal digits                 | `TRUNC(123.456, 2) → 123.45`        |
| `MOD()`     | Remainder of division                    | `MOD(10, 3) → 1`                    |
| `ABS()`     | Absolute value                           | `ABS(-10) → 10`                      |
| `CEIL()`    | Smallest integer ≥ value                | `CEIL(4.2) → 5`                      |
| `FLOOR()`   | Largest integer ≤ value                 | `FLOOR(4.9) → 4`                     |

### 📅 Date Functions

| Function        | Purpose                                 | Example                                 |
|------------------|------------------------------------------|------------------------------------------|
| `SYSDATE`        | Current date/time                       | `SELECT SYSDATE FROM dual;`             |
| `CURRENT_DATE`   | Current date in session timezone        | `SELECT CURRENT_DATE FROM dual;`        |
| `ADD_MONTHS()`   | Adds months to a date                   | `ADD_MONTHS(SYSDATE, 3)`                |
| `MONTHS_BETWEEN()` | Months between two dates              | `MONTHS_BETWEEN('2025-12-01', '2025-01-01') → 11` |
| `NEXT_DAY()`     | Next weekday after given date           | `NEXT_DAY(SYSDATE, 'FRIDAY')`           |
| `LAST_DAY()`     | Last day of the month                   | `LAST_DAY(SYSDATE)`                     |
| `TRUNC(date)`    | Truncates time                          | `TRUNC(SYSDATE)`                        |

### 🧠 Conversion Functions

| Function      | Purpose                                | Example                              |
|---------------|-----------------------------------------|--------------------------------------|
| `TO_CHAR()`   | Converts date/number to string         | `TO_CHAR(SYSDATE, 'YYYY-MM-DD')`     |
| `TO_DATE()`   | Converts string to date                | `TO_DATE('2025-05-16', 'YYYY-MM-DD')`|
| `TO_NUMBER()` | Converts string to number              | `TO_NUMBER('123')`                   |
| `CAST()`      | Converts data type                     | `CAST('2025-01-01' AS DATE)`         |

### 🧮 Aggregate Functions

| Function     | Purpose                                | Example                                      |
|--------------|-----------------------------------------|----------------------------------------------|
| `SUM()`      | Adds values                            | `SELECT SUM(salary) FROM employees;`        |
| `AVG()`      | Averages values                        | `SELECT AVG(salary) FROM employees;`        |
| `MAX()`      | Highest value                          | `SELECT MAX(salary) FROM employees;`        |
| `MIN()`      | Lowest value                           | `SELECT MIN(salary) FROM employees;`        |
| `COUNT()`    | Row or value count                     | `SELECT COUNT(*) FROM employees;`           |
| `GROUP BY`   | Aggregates based on grouped column     | `SELECT dept, SUM(salary) FROM emp GROUP BY dept;` |

---

## 📦 Oracle Built-in Packages

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

## ✅ Notes

- Use `SELECT * FROM dual;` to test most scalar SQL functions.
- Many APEX utilities require appropriate privileges or to be used inside application logic.

---

