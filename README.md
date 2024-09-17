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

