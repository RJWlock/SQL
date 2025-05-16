# Oracle SQL & APEX Keywords Cheat Sheet

This document provides a quick reference to common Oracle SQL, PL/SQL, and APEX keywords along with descriptions and examples. Use it to help understand basic syntax, data definition, and manipulation commands, as well as APEX-specific functionality.

---

## 1. SQL Keywords

These keywords are the foundation for querying and managing data:

| **Keyword** | **Description** | **Example** |
| ----------- | --------------- | ----------- |
| `SELECT`    | Retrieves data from a table or view. | `SELECT * FROM employees;` |
| `FROM`      | Specifies the table or view from which to retrieve data. | `SELECT name FROM employees;` |
| `WHERE`     | Filters rows based on specified conditions. | `SELECT * FROM employees WHERE salary > 50000;` |
| `INSERT`    | Adds new rows into a table. | `INSERT INTO employees (name, salary) VALUES ('John', 60000);` |
| `UPDATE`    | Modifies existing table rows. | `UPDATE employees SET salary = 65000 WHERE name = 'John';` |
| `DELETE`    | Removes rows from a table. | `DELETE FROM employees WHERE name = 'John';` |
| `JOIN`      | Combines rows from two or more tables based on a related column. | `SELECT e.name, d.dept_name FROM employees e JOIN departments d ON e.dept_id = d.id;` |

---

## 2. Data Definition Language (DDL)

DDL commands define and manage schema objects:

| **Keyword** | **Description** | **Example** |
| ----------- | --------------- | ----------- |
| `CREATE`    | Creates a new database object (e.g., table, view, index). | `CREATE TABLE employees (id NUMBER, name VARCHAR2(50));` |
| `ALTER`     | Modifies an existing object (e.g., adding a column). | `ALTER TABLE employees ADD (department_id NUMBER);` |
| `DROP`      | Deletes an object (e.g., table, index). | `DROP TABLE employees;` |
| `TRUNCATE`  | Removes all rows from a table, resetting it. | `TRUNCATE TABLE employees;` |

---

## 3. Data Manipulation Language (DML)

DML commands manage and manipulate actual data:

| **Keyword** | **Description** | **Example** |
| ----------- | --------------- | ----------- |
| `INSERT`    | Adds new rows into a table. | `INSERT INTO employees (name, salary) VALUES ('Alice', 75000);` |
| `UPDATE`    | Changes data in existing rows. | `UPDATE employees SET salary = 80000 WHERE name = 'Alice';` |
| `DELETE`    | Deletes existing rows. | `DELETE FROM employees WHERE name = 'Alice';` |
| `MERGE`     | Combines INSERT and UPDATE operations. | <pre>MERGE INTO employees e<br>USING (SELECT id, salary FROM temp) t<br>ON (e.id = t.id)<br>WHEN MATCHED THEN<br>  UPDATE SET e.salary = t.salary<br>WHEN NOT MATCHED THEN<br>  INSERT (id, salary) VALUES (t.id, t.salary);</pre> |
| `LOCK`      | Locks a table or row to ensure transactional consistency. | `LOCK TABLE employees IN EXCLUSIVE MODE;` |

---

## 4. Transaction Control

These keywords are used to manage transactions:

| **Keyword** | **Description** | **Example** |
| ----------- | --------------- | ----------- |
| `COMMIT`    | Finalizes the current transaction. | `COMMIT;` |
| `ROLLBACK`  | Reverses changes made during the current transaction. | `ROLLBACK;` |
| `SAVEPOINT` | Sets a point to which you can later roll back. | `SAVEPOINT before_update;` |
| `SET TRANSACTION` | Configures transaction options such as isolation levels. | `SET TRANSACTION ISOLATION LEVEL READ COMMITTED;` |

---

## 5. PL/SQL Keywords

PL/SQL extends SQL with programming constructs:

| **Keyword** | **Description** | **Example** |
| ----------- | --------------- | ----------- |
| `DECLARE`   | Begins a PL/SQL block for declaring variables. | `DECLARE v_salary NUMBER;` |
| `BEGIN`     | Starts the executable section of a PL/SQL block. | `BEGIN v_salary := 60000; END;` |
| `END`       | Marks the end of a PL/SQL block. | `BEGIN DBMS_OUTPUT.PUT_LINE('Hello'); END;` |
| `IF`        | Starts a conditional statement. | `IF v_salary > 50000 THEN DBMS_OUTPUT.PUT_LINE('High'); END IF;` |
| `LOOP`      | Creates a loop construct. | `LOOP<br>  EXIT WHEN condition;<br>END LOOP;` |
| `EXCEPTION` | Begins an exception handling section. | `BEGIN ... EXCEPTION WHEN NO_DATA_FOUND THEN DBMS_OUTPUT.PUT_LINE('Not Found'); END;` |

---

## 6. Data Types

Oracle SQL uses data types to enforce data integrity:

| **Keyword** | **Description** | **Example** |
| ----------- | --------------- | ----------- |
| `NUMBER`    | For numeric values (both integer and decimal). | `salary NUMBER(8,2)` |
| `VARCHAR2`  | Variable-length character strings. | `name VARCHAR2(100)` |
| `DATE`      | Stores date and time values. | `hire_date DATE` |
| `CLOB`      | Stores large character objects. | `description CLOB` |
| `BLOB`      | Stores binary large objects. | `image BLOB` |

---

## 7. Oracle APEX-Specific Keywords

These keywords and bind variables are specific to Oracle APEX applications:

| **Keyword**    | **Description** | **Example** |
| -------------- | --------------- | ----------- |
| `:APP_ID`      | Holds the application ID during an APEX session. | Usage in page validations or computations: `:APP_ID` |
| `:APP_PAGE_ID` | Contains the current page ID in APEX. | Useful for dynamic computations: `:APP_PAGE_ID` |
| `APEX_UTIL`    | Package providing utility procedures. | `APEX_UTIL.SET_SESSION_STATE('MY_ITEM', 'value');` |
| `APEX_ITEM`    | Package used to create dynamic form elements. | `APEX_ITEM.TEXT(1, p_value)` |
| `APEX_MAIL`    | Package to send emails from APEX. | `APEX_MAIL.SEND(p_to => 'user@example.com', p_body => 'Hello');` |

---

## 8. Common Oracle Functions

Oracle built-in functions that perform calculations, conversions, and more:

| **Function** | **Description** | **Example** |
| ------------ | --------------- | ----------- |
| `SYSDATE`    | Returns the current date and time. | `SELECT SYSDATE FROM dual;` |
| `TO_DATE`    | Converts a string to a date. | `TO_DATE('2025-05-16','YYYY-MM-DD')` |
| `NVL`        | Substitutes a value when a NULL is encountered. | `SELECT NVL(commission, 0) FROM employees;` |
| `UPPER`      | Converts text to uppercase. | `SELECT UPPER(name) FROM employees;` |
| `SUBSTR`     | Extracts a substring from text. | `SELECT SUBSTR('Oracle SQL', 1, 6) FROM dual;` |

---

## 9. System Privileges & Roles

Keywords for granting or revoking user permissions:

| **Keyword** | **Description** | **Example** |
| ----------- | --------------- | ----------- |
| `GRANT`     | Provides users with specific privileges. | `GRANT SELECT ON employees TO hr_user;` |
| `REVOKE`    | Removes previously granted privileges. | `REVOKE SELECT ON employees FROM hr_user;` |
| `CREATE SESSION` | Allows a user to log in to the database. | Typically granted during user creation. |
| `DBA`       | A high-level role with broad privileges. | `GRANT DBA TO admin_user;` |

---

## 10. Hints

Hints are suggestions to the Oracle optimizer about how to execute a query:

| **Hint**    | **Description** | **Example** |
| ----------- | --------------- | ----------- |
| `INDEX`     | Suggests using an index to optimize query performance. | `SELECT /*+ INDEX(employees emp_idx) */ * FROM employees;` |
| `PARALLEL`  | Enables parallel execution for a query. | `SELECT /*+ PARALLEL(employees, 4) */ * FROM employees;` |
| `FULL`      | Forces a full table scan. | `SELECT /*+ FULL(employees) */ * FROM employees;` |

---

## Additional Resources

- **Oracle Database SQL Language Reference:** Explore Oracle’s official documentation for detailed syntax and features.
- **Oracle APEX Documentation:** Find examples, tutorials, and detailed explanations on building APEX applications.

---

## How to Use This Cheat Sheet

1. **Copy/Paste:** Copy the entire content from this file and paste it into your project’s repository as `oracle_keywords_cheatsheet.md`.
2. **Customization:** Modify or extend the cheat sheet to fit the version of Oracle or specific project requirements.
3. **Further Reading:** Use the resources listed above to dive deeper into any topics as needed.

---

*Note:* The provided keywords, descriptions, and examples are meant as a quick guide. Oracle’s full feature set includes many more functions, data types, and options that you can find in the official documentation.

