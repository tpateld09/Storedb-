# Shopping Store SQL — Many-to-Many Relationship

## 1. Project Overview / Objective

This is my **second SQL learning project**, created to practice **one-to-many and many-to-many relationships** using PostgreSQL.

The project uses four tables — `customers`, `orders`, `products`, and `order_items` — to model a simple shopping-store database and retrieve customer order details along with the products purchased.

---

## 2. Database Design

The database contains four related tables:

- `customers` — stores customer details
- `orders` — stores customer orders
- `products` — stores product names and prices
- `order_items` — connects orders with products and stores the quantity purchased

### SQL Table Creation

```sql
--customers
CREATE TABLE customers 
(
    cust_id SERIAL PRIMARY KEY,
    cust_name VARCHAR(100) NOT NULL
);

INSERT INTO customers (cust_name)
VALUES ('Raju'), ('Sham'), ('Paul'), ('Alex');
 
 --orders
CREATE TABLE orders 
(
    ord_id SERIAL PRIMARY KEY,
    ord_date DATE NOT NULL,
    cust_id INTEGER NOT NULL,
    FOREIGN KEY (cust_id) REFERENCES customers(cust_id)
);

INSERT INTO orders (ord_date, cust_id)
VALUES
    ('2024-01-01', 1),  -- Raju first order
    ('2024-02-01', 2),  -- Sham first order
    ('2024-03-01', 3),  -- Paul first order
    ('2024-04-04', 2);  -- Sham second order

--products 
CREATE TABLE products 
(   
     P_id SERIAL PRIMARY KEY,
	 p_name VARCHAR(100) NOT NULL,
	 price NUMERIC NOT NULL
);

INSERT INTO products (p_name, price)
VALUES
    ('Laptop', 55000.00),
    ('Mouse', 500),
    ('Keyboard', 800.00),
    ('Cable', 250.00)
;


--ORDER_ITEMS
CREATE TABLE order_items 
(   
   items_id SERIAL PRIMARY KEY,
	 ord_id INT NOT NULL,
	 p_id INT NOT NULL,
	 quantity INT NOT NULL,
	 FOREIGN KEY (ord_id) REFERENCES orders(ord_id),
     FOREIGN KEY (p_id) REFERENCES products(P_id)
);

INSERT INTO order_items (ord_id, p_id, quantity)
VALUES
    (1, 1, 1),  -- Raju ordered 1 Laptop
    (1, 4, 2),  -- Raju ordered 2 Cables
    (2, 1, 1),  -- Sham ordered 1 Laptop
    (3, 2, 1),  -- Paul ordered 1 Mouse
    (3, 4, 5),  -- Paul ordered 5 Cables
    (4, 3, 1);  -- Sham ordered 1 Keyboard
 
```
## 3.Relationship Design
One-to-Many

One customer can place multiple orders.
<img width="707" height="302" alt="Screenshot 2026-09-22 132911" src="https://github.com/user-attachments/assets/8bf6b26f-14b9-4020-aff6-9e1492bec37e" />

Many-to-Many
One order can contain multiple products, and one product can appear in multiple orders.

The order_items table acts as the bridge table.
<img width="1006" height="622" alt="Screenshot 2026-09-22 132751" src="https://github.com/user-attachments/assets/2b6ef113-1760-4f08-bc3b-2559f5efbf53" />

### Final Query
```
SELECT 
       c.cust_name, 
       o.ord_date, 
	     p.p_name,
	     p.price, 
	     oi.quantity,
	     oi.quantity*p.price as total_price 
 FROM order_items oi 
    INNER JOIN
	    products p ON oi.p_id=p.p_id
	  INNER JOIN
	      orders o ON o.ord_id=oi.ord_id
	  INNER JOIN 
	      customers c ON o.cust_id=c.cust_id;
```
## 5. Result
The final query successfully combines the four tables and displays customer, order, product, quantity, price, and total price.
<img width="910" height="446" alt="Screenshot 2026-09-22 144813" src="https://github.com/user-attachments/assets/e35180e1-dbf0-492e-aac6-1f6144a9f569" />

## 6. Learning & What I Learned
Through this project, I learned how to:

--Create related tables using Primary Keys and Foreign Keys
--Understand one-to-many relationships
--Implement many-to-many relationships using a bridge table
--Use JOIN to combine data from multiple tables
--Create calculated columns using SQL expressions
