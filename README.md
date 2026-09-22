# Shopping Store SQL --- Relationships Project

## Project Overview

**Project**: Shopping Store Database --- One-to-Many & Many-to-Many
Relationships
**Project Type**: SQL Learning Project
**Project Number**: 2
**Database**: PostgreSQL
**Level**: Beginner / Intermediate SQL Practice

This project is a small PostgreSQL database designed to practice how
multiple related tables work together in a shopping-store context.

~~~The project uses four tables:

customers

orders

products

order_items
~~~

The main focus is understanding Primary Keys, Foreign Keys,
one-to-many relationships, many-to-many relationships, JOINs, and
calculated values.

1. ## Project Objective

Create a small shopping-store database using SQL to demonstrate
one-to-many and many-to-many relationships using four related
tables.

The database should allow us to connect:

Customers with their orders
Orders with the products they contain
Products with their prices
Quantities of products purchased in each order

The final query should display the customer, order, product, quantity,
price, and total price for each order item.

2. ## Database Design

### Customers

Stores information about customers.

Column        Description

cust_id     Primary key identifying each customer
cust_name   Customer name
~~~



~~~


### Orders

Stores information about orders placed by customers.

Column       Description

ord_id     Primary key identifying each order
ord_date   Date of the order
cust_id    Foreign key referencing customers

### Products

Stores information about products available in the store.

Column     Description

p_id     Primary key identifying each product
p_name   Product name
price    Price of the product

### Order_Items

Acts as the bridge/junction table between orders and products.

Column       Description

items_id   Primary key identifying each order-item record
ord_id     Foreign key referencing orders
p_id       Foreign key referencing products
quantity   Quantity of the product purchased

3. ## Relationship Design
<img width="1487" height="401" alt="Screenshot 2026-09-21 215111" src="https://github.com/user-attachments/assets/a20c65b8-5d10-4424-97ad-2f15fb27c639" />

