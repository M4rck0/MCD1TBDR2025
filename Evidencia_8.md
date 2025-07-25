# 📝 Tarea 8 — Base de Datos Chinook (MySQL)

---

## Vistas (VIEW) con diferentes tipos de JOIN y subconsultas


### 🔹 1. Vista con `INNER JOIN`
Lista todos los clientes, incluso aquellos que aún no han generado facturas.

```sql
CREATE VIEW Vista_Join AS
SELECT a.AlbumId, a.Title AS AlbumTitle, ar.Name AS ArtistName
FROM Album a
JOIN Artist ar ON a.ArtistId = ar.ArtistId;
```



### 🔹 2. Vista con `LEFT JOIN`
Lista todos los clientes, incluso aquellos que aún no han generado facturas.

```sql
CREATE VIEW Vista_LeftJoin AS
SELECT c.CustomerId, c.FirstName, c.LastName, i.InvoiceId
FROM Customer c
LEFT JOIN Invoice i ON c.CustomerId = i.CustomerId;
```



### 🔹 3. Vista con `RIGHT JOIN`
Muestra los empleados y los clientes que tienen asignados como representantes de soporte.

```sql
CREATE VIEW Vista_RightJoin AS
SELECT e.EmployeeId, e.FirstName, c.CustomerId, c.FirstName AS CustomerFirstName
FROM Employee e
RIGHT JOIN Customer c ON e.EmployeeId = c.SupportRepId;
```



### 🔹 4. Vista con subconsulta
Devuelve los clientes que han generado más de 5 facturas.

```sql
CREATE VIEW Vista_Subconsulta AS
SELECT FirstName, LastName
FROM Customer
WHERE CustomerId IN (
  SELECT CustomerId
  FROM Invoice
  GROUP BY CustomerId
  HAVING COUNT(*) > 5
);
```
