# Online Store PostgreSQL - Sorine Lachichi
## _Mis à jour le 17/09/2024_

## Diagramme
![Main](https://github.com/user-attachments/assets/0cc05981-a163-41d1-8a59-c2534f6739ec)



---

# Command History and Explanations

This section describes the commands used to configure the online_store database in PostgreSQL via LibreOffice Base.

### 1. Connect to PostgreSQL 
Pour se connecter à PostgreSQL en tant qu'utilisateur `postgres`, utilisez la commande suivante dans le terminal :
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
