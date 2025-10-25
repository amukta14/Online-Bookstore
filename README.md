

##  Online Bookstore Database Project

[cite\_start]The project followed a Structured Database Development Lifecycle (SDLC) to address core operational challenges, including inefficient data management, poor inventory tracking, and cumbersome order processing[cite: 7, 9, 14].

-----

## Project Objectives

[cite\_start]The primary goal was to create a robust and streamlined system capable of[cite: 8]:

  * [cite\_start]Managing essential information about books, authors, publishers, customers, orders, and inventory[cite: 16].
  * [cite\_start]Ensuring accurate stock levels and product availability[cite: 18].
  * [cite\_start]Streamlining order processing and tracking to enhance customer satisfaction[cite: 19].
  * [cite\_start]Maintaining high data quality and integrity through constraints and validation[cite: 21].

-----

## Database Design and Schema

[cite\_start]The database architecture is based on the Entity-Relationship (ER) model [cite: 22] and normalized into the following relational schema:

### Entities and Relationships

| Entity | Primary Key (PK) | Key Relationships | Cardinality |
| :--- | :--- | :--- | :--- |
| **Book** | `book_id` | [cite\_start]**$\leftrightarrow$ Author** (Written By) [cite: 123] | [cite\_start]Many-to-Many ($M:N$) [cite: 123] |
| **Publisher** | `publisher_id` | [cite\_start]**$\leftrightarrow$ Book** (Published By) [cite: 124] | [cite\_start]One-to-Many ($1:N$) [cite: 142] |
| **Customer** | `customer_id` | [cite\_start]**$\leftrightarrow$ Order** (Placed By) [cite: 154] | [cite\_start]One-to-Many ($1:N$) [cite: 154] |
| **Inventory** | `book_id` | [cite\_start]**$\leftrightarrow$ Book** (Has Inventory) [cite: 125] | [cite\_start]One-to-One ($1:1$) [cite: 125] |

### Implementation and Integrity Constraints (DDL)

[cite\_start]The schema was implemented using DDL, incorporating critical constraints for data integrity[cite: 480]:

| Table | Primary Key | Foreign Key Reference(s) | Unique Constraint | Other Constraints |
| :--- | :--- | :--- | :--- | :--- |
| **`Book`** | `book_id` | [cite\_start]`publisher_id` (Publisher) [cite: 215] | N/A | N/A |
| **`Customer`** | `customer_id` | N/A | [cite\_start]`email` [cite: 222] | N/A |
| **`Inventory`** | `book_id` | [cite\_start]`book_id` (Book) [cite: 237] | N/A | [cite\_start]`CHECK (stock >= 0)` [cite: 236] |
| **`Written_By`** | (`book_id`, `author_id`) | [cite\_start]`book_id` (Book), `author_id` (Author) [cite: 256, 257, 258] | N/A | N/A |
| **`Contains`** | (`order_id`, `book_id`) | [cite\_start]`order_id` (Order), `book_id` (Book) [cite: 266, 267, 268] | N/A | N/A |

-----

## Core SQL and PL/SQL Features

### 1\. Advanced Queries (GROUP BY, ORDER BY, HAVING)

These structured queries facilitate reporting and data analysis based on aggregation:

| Objective | SQL Concept | Description |
| :--- | :--- | :--- |
| **Publisher Analytics** | **`GROUP BY`** | [cite\_start]Retrieves the name of each publisher and the total count of their books[cite: 360, 361]. |
| **Price Analysis** | **`ORDER BY`** | [cite\_start]Lists book genres and their respective average prices, ordered from highest to lowest[cite: 371, 372]. |
| **Author Productivity** | **`HAVING`** | [cite\_start]Identifies authors who have authored more than one book by filtering aggregate counts[cite: 382, 383]. |

### 2\. Triggers: Automated Inventory Management

[cite\_start]A **trigger** (`trg_update_inventory`) was created to enforce a critical business rule automatically upon data modification[cite: 404, 405].

  * [cite\_start]**Purpose:** To automate inventory stock level updates[cite: 481].
  * **Mechanism:** An `AFTER INSERT` trigger is placed on the **`Contains`** table. [cite\_start]When a book is added to an order, the trigger automatically executes an `UPDATE` statement to decrement the `stock` in the **`Inventory`** table by the ordered quantity (`:NEW.quantity`)[cite: 407, 410, 411, 412].

<!-- end list -->

```sql
CREATE OR REPLACE TRIGGER trg_update_inventory
 AFTER INSERT ON Contains
 FOR EACH ROW
 BEGIN
     UPDATE Inventory
     SET stock = stock - :NEW.quantity
     WHERE book_id = :NEW.book_id;
 END;
```

### 3\. Cursors: Row-Level Control

[cite\_start]Cursors are demonstrated in PL/SQL to manage result sets and process data row-by-row, ensuring detailed control over data manipulation[cite: 434].

  * [cite\_start]**Implicit Cursor:** Automatically created by the database for single SQL statements (e.g., `UPDATE`)[cite: 429, 430]. [cite\_start]The demonstration uses `SQL%ROWCOUNT` to report the number of fantasy books whose price was updated[cite: 447, 453].
  * [cite\_start]**Explicit Cursor:** Manually declared and controlled for handling queries that return multiple rows[cite: 432, 433]. [cite\_start]The demonstration uses an explicit cursor (`c_customer_cursor`) to iterate through and display the ID and name of customers residing in 'Mumbai'[cite: 461, 464, 468, 470, 472].
