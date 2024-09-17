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
