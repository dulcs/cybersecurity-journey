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
### Lab 1: SQL Injection Vulnerability in WHERE Clause Allowing Retrieval of Hidden Data

* **Objective:** Perform a SQL injection attack that causes the application to display one or more unreleased products.
* 
* **Methodology & Payloads:**
    1. Navigated to the main application and selected a specific category filter (in this case, `Gifts`).
    2. Appended the payload `' OR 1=1--` directly to the URL parameter in the browser's address bar:
       ```sql
       /filter?category=Gifts' OR 1=1--
       ```
    3. The database evaluated the conditional statement as a tautology (`OR 1=1`), forcing the query to return every row in the table and successfully rendering the hidden items on the screen.

	#### 🧠 Technical Insight: Input Context & Data Types 
	* **Integer Parameters (`productId=10`):** Often implement strict data-type validation at the application layer. Injecting strings or quotes triggers an immediate error before the input can interact with the database engine. 
	* **String Parameters (`category=Gifts`):** Highly vulnerable to direct string concatenation if unsanitized. This context allows the single quote (`'`) to successfully break the query structure and execute the malicious payload logic.

* **Evidence / Flag:**
    ![[Pasted image 20260618020315.png]]


## 🛡️ Defensive Mitigations (Secure Coding)
*   **Defensive Standard:** Implement **Parameterized Queries (Prepared Statements)**. This ensures the database engine treats user input strictly as a literal value, never as executable code logic.