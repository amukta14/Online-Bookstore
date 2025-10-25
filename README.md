
# Online Bookstore Database Project

A streamlined database solution for efficient online bookstore management, addressing key operational challenges such as data organization, inventory tracking, customer satisfaction, and order processing.[1]

***

## Table of Contents

- Overview
- Features
- Database Design
- Entity Descriptions
- Schema: Tables & Relationships
- Sample Data
- SQL Queries & Business Logic
- Triggers and Cursors
- Contributors

***

## Overview

This project solves typical inefficiencies faced by online bookstores by providing a robust schema to manage books, authors, publishers, customers, orders, and stock inventory. It ensures seamless data flow and enhances the end-user experience with comprehensive reporting and accurate stock management.[1]

***

## Features

- Organized management of books, authors, publishers, customers, orders, and inventory
- User-friendly search and browsing for titles and genres
- Streamlined, simple order and checkout processes
- Accurate, real-time stock availability tracking
- Reports on sales trends and customer activity
- Enforced data integrity via constraints and validation rules[1]

***

## Database Design

The solution is modeled using an Entity-Relationship (ER) diagram focusing on the following entities:

- Book
- Author
- Publisher
- Customer
- Order
- Inventory

Each entity is mapped to a relational table, capturing real-world business workflow in a normalized, scalable database structure.[1]

***

## Entity Descriptions

| Entity     | Purpose                                             | Key Attributes                                             |
|------------|-----------------------------------------------------|------------------------------------------------------------|
| Book       | All book details                                    | BookID, Title, AuthorID, PublisherID, Genre, Price, Year   |
| Author     | Author information                                  | AuthorID, Name, Nationality, Bio                           |
| Publisher  | Publishing company details                          | PublisherID, Name, Address, Contact, Email                 |
| Customer   | Customer accounts and orders                        | CustomerID, Name, Address, Email, Phone, RegistrationDate  |
| Order      | Online orders placed by customers                   | OrderID, CustomerID, OrderDate, TotalAmount, PaymentMethod, ShippingAddress |
| Inventory  | Stock levels for each book                          | BookID, Stock                                              |
[1]

***

## Schema: Tables & Relationships

- Tables created using standard SQL DDL.
- Relationships enforced via primary and foreign keys.
- Many-to-many and one-to-many relationships via linking tables such as WrittenBy and Contains.[1]

**Sample table creation:**

```sql
CREATE TABLE Book (
    bookid INT PRIMARY KEY,
    title VARCHAR(150),
    genre VARCHAR(50),
    price DECIMAL(8,2),
    publicationyear YEAR,
    publisherid INT,
    FOREIGN KEY (publisherid) REFERENCES Publisher(publisherid)
);
```
Additional tables include Author, Publisher, Customer, Inventory, Order, WrittenBy, and Contains with appropriate constraints and keys.

***

## Sample Data

The project includes meaningful initial data for all tables:

- Publishers (e.g., Pearson, Penguin, HarperCollins)
- Authors (e.g., J.K. Rowling, George Orwell)
- Books (e.g., Harry Potter, 1984, Da Vinci Code)
- Customers, Orders, Inventory levels, etc.[1]

***

## SQL Queries & Business Logic

- Retrieve publisher names with book counts
- List genres by average price (descending)
- Find authors with more than one book
- Demonstration of GROUP BY, ORDER BY, and HAVING SQL clauses

***

## Triggers and Cursors

- Example trigger to auto-update inventory after order placement
- Implicit and explicit cursor usage for automated or granular data handling

***

## License

For educational use. Adapt and expand as needed.

***

This README distills your project into clear, reader-friendly sections suitable for technical presentation or GitHub repository documentation.[1]

[1](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/78966423/60d2d00d-ac76-4c4e-9903-bc006dc3c372/Online-Bookstore-PPT-1.pdf)
