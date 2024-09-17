# Online Store PostgreSQL - Sorine Lachichi


## Diagramme
![Main](https://github.com/user-attachments/assets/0cc05981-a163-41d1-8a59-c2534f6739ec)



---

# Command History and Explanations

This section describes the commands used to configure the online_store database in PostgreSQL via LibreOffice Base.

### 1. Connect to PostgreSQL 
To connect to PostgreSQL as the postgres user, use the following command in the terminal::
```msdos
psql -U postgres 
```

### 2. Create database and connect (always as the `postgres` user)
```sql
CREATE DATABASE online_store;
\c online_store;
```
### 3. Write the SQL Query to Create the Table
#### My tables:
##### Customers:
```sql
CREATE TABLE "Customers" (
    "CustomerID" SERIAL PRIMARY KEY,
    "Name" VARCHAR(100) NOT NULL,
    "Email" VARCHAR(100) UNIQUE NOT NULL,
    "Address" TEXT,
    "Phone" VARCHAR(15)
```
##### Orders:
```sql
CREATE TABLE "Orders" (
    "OrderID" SERIAL PRIMARY KEY,
    "OrderDate" DATE DEFAULT CURRENT_DATE,
    "TotalAmount" DECIMAL(10, 2) NOT NULL,
    "CustomerID" INTEGER NOT NULL,
    FOREIGN KEY ("CustomerID") REFERENCES "Customers"("CustomerID") ON DELETE CASCADE
);
```
##### order Details:
```sql
CREATE TABLE "OrderDetails" (
    "OrderDetailID" SERIAL PRIMARY KEY,
    "OrderID" INTEGER NOT NULL,
    "ProductID" INTEGER NOT NULL,
    "Quantity" INTEGER NOT NULL,
    FOREIGN KEY ("OrderID") REFERENCES "Orders"("OrderID") ON DELETE CASCADE,
    FOREIGN KEY ("ProductID") REFERENCES "Products"("ProductID") ON DELETE CASCADE
);
```
##### Payments:
```sql
CREATE TABLE "Payments" (
    "PaymentID" SERIAL PRIMARY KEY,
    "PaymentDate" DATE DEFAULT CURRENT_DATE,
    "Amount" DECIMAL(10, 2) NOT NULL,
    "OrderID" INTEGER NOT NULL,
    FOREIGN KEY ("OrderID") REFERENCES "Orders"("OrderID") ON DELETE CASCADE
);
```
##### Products:
```sql
CREATE TABLE "Products" (
    "ProductID" SERIAL PRIMARY KEY,
    "Name" VARCHAR(100) NOT NULL,
    "Price" DECIMAL(10, 2) NOT NULL,
    "Stock" INTEGER,
    "Description" TEXT
);
```
### 4. Execute the SQL Query
Click on "Run" (the icon representing a play button or a similar button) to execute the SQL query.
If the query is executed correctly, the table will be created in your database.

### 5. Verify the Table Creation
In the left navigation pane, click on "Tables" to check that the new table appears in the list of tables.

### 6. Add Data
#### My DATA:
##### Customers:
```sql
INSERT INTO "Customers" ("Name", "Email", "Address", "Phone")
VALUES
    ('Theo Johnson', 'theo.johnson@example.com', '123 Pine Road', '555-6789'),
    ('Amine Karim', 'amine.karim@example.com', '456 Cedar Street', '555-9876'),
    ('Marvine Lee', 'marvine.lee@example.com', '789 Birch Avenue', '555-5432');
```

##### Order:
```sql
INSERT INTO "Orders" ("OrderDate", "TotalAmount", "CustomerID")
VALUES
    ('2024-09-15', 1200.00, 1), 
    ('2024-09-16', 800.00, 2),   
    ('2024-09-17', 150.00, 3);   
```
##### Order Details:
```sql
INSERT INTO "OrderDetails" ("OrderID", "ProductID", "Quantity")
VALUES
    (1, 1, 1),  
    (2, 2, 1),  
    (3, 3, 1);
```
##### Payments:
```sql
INSERT INTO "Payments" ("PaymentDate", "Amount", "OrderID")
VALUES
    ('2024-09-16', 1200.00, 1),  
    ('2024-09-17', 800.00, 2),  
    ('2024-09-18', 150.00, 3);
```
##### Product:
```sql
INSERT INTO "Products" ("Name", "Price", "Stock", "Description")
VALUES
    ('Laptop', 1200.00, 15, 'High-performance laptop with 16GB RAM'),
    ('Smartphone', 800.00, 30, 'Latest model smartphone with 128GB storage'),
    ('Headphones', 150.00, 50, 'Noise-cancelling over-ear headphones'),
    ('Monitor', 300.00, 20, '27-inch 4K monitor');

```
### View the tables:
#### Customers:
<img width="438" alt="image" src="https://github.com/user-attachments/assets/173b59c0-7d19-47ef-8127-3919ed3e946d">

#### Order:
<img width="319" alt="image" src="https://github.com/user-attachments/assets/df70f47e-c7ec-4739-8dc7-3a61eeb81fb7">


#### Order Details:
<img width="328" alt="image" src="https://github.com/user-attachments/assets/5a698d90-cf32-4191-a29b-9426aa67037f">

#### Products:
<img width="341" alt="image" src="https://github.com/user-attachments/assets/989c7ba0-8217-49c6-bada-5a10e087330a">


#### Payments:
<img width="350" alt="image" src="https://github.com/user-attachments/assets/b504a9a8-760d-40d3-8edb-d5707854a528">

### 7. Some simple Queries:
#### Stock Product:
```sql
SELECT "Name", "Stock"
FROM "Products";
```
##### screenshot:
<img width="266" alt="image" src="https://github.com/user-attachments/assets/94650024-6194-49f8-8df3-c29b0908f606">

#### Product quantities for specific order:
```sql
SELECT "Products"."Name", "OrderDetails"."Quantity"
FROM "OrderDetails"
JOIN "Products" ON "OrderDetails"."ProductID" = "Products"."ProductID"
WHERE "OrderDetails"."OrderID" = 1;
```
##### screenshot:
<img width="445" alt="image" src="https://github.com/user-attachments/assets/89c004ad-3f7f-402d-a652-3e93d104dd8b">

#### Product list with description:
```sql
SELECT "Name", "Description"
FROM "Products";
```
##### screenshot:
<img width="385" alt="image" src="https://github.com/user-attachments/assets/e6395f30-7d39-4732-9dc0-9948e00368a9">

#### Payment Details and Associated Orders:
```sql
SELECT "Payments"."PaymentDate", "Payments"."Amount", "Orders"."OrderID"
FROM "Payments"
JOIN "Orders" ON "Payments"."OrderID" = "Orders"."OrderID";
```
##### screenshot:
<img width="457" alt="image" src="https://github.com/user-attachments/assets/4bc349a9-c87d-4309-9f9b-92ff814a07b1">

#### Customers Numer of Order:
```sql
SELECT "Customers"."Name" AS "CustomerName", COUNT("Orders"."OrderID") AS "NumberOfOrders"
FROM "Customers"
LEFT JOIN "Orders" ON "Customers"."CustomerID" = "Orders"."CustomerID"
GROUP BY "Customers"."CustomerID"
ORDER BY "NumberOfOrders" DESC;
```
##### screenshot:
<img width="589" alt="image" src="https://github.com/user-attachments/assets/d5f2788e-29b4-4e7a-971f-0a7e849c01fc">


