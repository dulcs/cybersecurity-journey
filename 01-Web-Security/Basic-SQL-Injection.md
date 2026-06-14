# 💉 Basic SQL Injection (SQLi)

## 🧠 Core Logical Mechanism (The "Why")
*   **Definition:** A vulnerability that occurs when user-supplied data is directly concatenated into a database query string instead of being handled separately.
*   **Design Flaw:** The application fails to properly sanitize or parameterize inputs, causing the SQL interpreter to mistake data for executable commands.

## 🛠️ Common Attack Vectors & Payloads
*   `' OR 1=1--` -> Bypasses authentication logic by forcing the conditional statement to evaluate as true.
*   `' UNION SELECT NULL--` -> Exploits the UNION operator to determine column counts or extract unauthorized data from adjacent tables.


## 🔬 Payload Analysis: `' OR 1=1--`
Behind the application, a vulnerable query might look like this:
```sql
SELECT * FROM products WHERE category = 'USER_INPUT' AND released = 1;

```


When injecting `' OR 1=1--`, the query breaks down logically as follows:

1. **The Single Quote (`'`)**: Prematurely closes the developer's intended data string, forcing the database engine to interpret the input as an empty value (`''`).
    
2. **The `OR` Operator**: Introduces an alternative logical condition to the `WHERE` clause.
    
3. **The Tautology (`1=1`)**: An equation that always resolves to `TRUE`. Since it is joined by an `OR`, the entire conditional check bypasses the original filters and evaluates as true for every single row in the table.
    
4. **The Comment Dash (`--`)**: Instructs the database engine to treat everything following it as a comment, effectively neutralizing the rest of the original query (`' AND released = 1;`).
    

## 🧪 Completed Laboratories (PortSwigger)

### Lab 1: [Lab Name Go Here]

- **Objective:**
    
- **Methodology & Payloads:**

*   **Evidence / Flag:** 

## 🛡️ Defensive Mitigations (Secure Coding)
*   **Defensive Standard:** Implement **Parameterized Queries (Prepared Statements)**. This ensures the database engine treats user input strictly as a literal value, never as executable code logic.