# 📝 Tarea 8 — Composición, vistas y disparadores

---

## Vistas (VIEW) con diferentes tipos de JOIN y subconsultas


### 🔹 1. Vista con `JOIN`
Lista todos los clientes, incluso aquellos que aún no han generado facturas.

```sql
CREATE VIEW Vista_Join AS
SELECT a.AlbumId, a.Title AS AlbumTitle, ar.Name AS ArtistName
FROM Album a
JOIN Artist ar ON a.ArtistId = ar.ArtistId;
```

Ejemplo del resultado:
| AlbumId | AlbumTitle                             | ArtistName |
|---------|----------------------------------------|------------|
| 1       | For Those About To Rock We Salute You  | AC/DC      |
| 2       | Balls to the Wall                      | Accept     |
| 3       | Restless and Wild                      | Accept     |
| 4       | Let There Be Rock                      | AC/DC      |
| 5       | Big Ones                               | Aerosmith  |



### 🔹 2. Vista con `LEFT JOIN`
Lista todos los clientes, incluso aquellos que aún no han generado facturas.

```sql
CREATE VIEW Vista_LeftJoin AS
SELECT c.CustomerId, c.FirstName, c.LastName, i.InvoiceId
FROM Customer c
LEFT JOIN Invoice i ON c.CustomerId = i.CustomerId;
```

Ejemplo del resultado:
| CustomerId | FirstName | LastName  | InvoiceId |
|------------|-----------|-----------|-----------|
| 1          | Luís      | Gonçalves | 98        |
| 1          | Luís      | Gonçalves | 121       |
| 1          | Luís      | Gonçalves | 143       |
| 1          | Luís      | Gonçalves | 195       |
| 1          | Luís      | Gonçalves | 316       |




### 🔹 3. Vista con `RIGHT JOIN`
Muestra los empleados y los clientes que tienen asignados como representantes de soporte.

```sql
CREATE VIEW Vista_RightJoin AS
SELECT e.EmployeeId, e.FirstName, c.CustomerId, c.FirstName AS CustomerFirstName
FROM Employee e
RIGHT JOIN Customer c ON e.EmployeeId = c.SupportRepId;
```

Ejemplo del resultado:
| EmployeeId | FirstName | CustomerId | CustomerFirstName |
|------------|-----------|------------|-------------------|
| 3          | Jane      | 1          | Luís              |
| 5          | Steve     | 2          | Leonie            |
| 3          | Jane      | 3          | François          |
| 4          | Margaret  | 4          | Bjørn             |
| 4          | Margaret  | 5          | František         |



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
Ejemplo del resultado:
| FirstName | LastName   |
|-----------|------------|
| Luís      | Gonçalves  |
| Leonie    | Köhler     |
| François  | Tremblay   |
| Bjørn     | Hansen     |
| František | Wichterlová|


---

## Crear un TRIGGER

### Paso 1: Crear la tabla de auditoría `bitacora_facturas`

Esta tabla almacenará el ID de la factura insertada, la fecha y hora del evento, y el tipo de acción realizada.

```sql
CREATE TABLE bitacora_facturas (
  id_bitacora INT AUTO_INCREMENT PRIMARY KEY,
  id_factura INT,
  fecha_evento TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  tipo_accion VARCHAR(50)
);
```



### Paso 2: Crear el trigger despues_insertar_factura

Este disparador se ejecutará automáticamente después de cada inserción en la tabla invoice y registrará el evento en bitacora_facturas.

```sql
DELIMITER $$

CREATE TRIGGER despues_insertar_factura
AFTER INSERT ON invoice
FOR EACH ROW
BEGIN
  INSERT INTO bitacora_facturas (id_factura, tipo_accion)
  VALUES (NEW.InvoiceId, 'INSERCIÓN');
END $$

DELIMITER ;
```

### Paso 3: Insertar una nueva factura de prueba

```sql
INSERT INTO invoice (InvoiceId, CustomerId, InvoiceDate, BillingAddress, BillingCity, BillingCountry, Total)
VALUES (1000, 1, NOW(), 'Av. Reforma 123', 'Ciudad de México', 'México', 200);
```

### Paso 4: Verificar los resultados

Consulta la tabla bitacora_facturas para comprobar que el trigger registró el evento correctamente:

```sql
SELECT * FROM bitacora_facturas;
```






