# Tarea 8 — Composición, vistas y disparadores

---

## Vistas (VIEW) con diferentes tipos de JOIN y subconsultas


### 🔹 1. Vista con `JOIN`
Lista todos los clientes, incluso aquellos que aún no han generado facturas.

```sql
CREATE VIEW vista_join AS
SELECT a.AlbumId, a.Title AS AlbumTitle, ar.Name AS ArtistName
FROM Album AS a
JOIN Artist AS ar ON a.ArtistId = ar.ArtistId;
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
CREATE VIEW vista_leftjoin AS
SELECT c.CustomerId, c.FirstName, c.LastName, i.InvoiceId
FROM Customer AS c
LEFT JOIN Invoice AS i ON c.CustomerId = i.CustomerId;
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
CREATE VIEW vista_rightjoin AS
SELECT e.EmployeeId, e.FirstName, c.CustomerId, c.FirstName AS CustomerFirstName
FROM Employee AS e
RIGHT JOIN Customer AS c ON e.EmployeeId = c.SupportRepId;
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
CREATE VIEW vista_subconsulta AS
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



### Paso 2: Crear el trigger `despues_insertar_factura`

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
VALUES (1000, 1, NOW(), 'Av. Georg Cantor', 'Ciudad de México', 'México', 100);
```

### Paso 4: Verificar los resultados

Consulta la tabla bitacora_facturas para comprobar que el trigger registró el evento correctamente:

```sql
SELECT * FROM bitacora_facturas;
```
Resultado:

| id_bitacora  | id_factura  | fecha_evento        | tipo_accion  |
| ------------ | ----------- | ------------------- | ------------ |
| 1            | 1000        | 2025-07-24 20:59:42 | INSERT       |



---

## Explicación de resultados y utilidad de vistas y disparador

### Vistas (VIEW)

Las vistas permiten encapsular consultas complejas y reutilizarlas como si fueran tablas. A continuación se resume el objetivo de cada una:

---

### Disparador (TRIGGER)

El disparador `despues_insertar_factura` registra automáticamente cada inserción en la tabla `invoice` dentro de una tabla llamada `bitacora_facturas`.

Esto permite:

- Llevar una **bitácora automatizada** sin intervención manual.
- Tener **evidencia de cambios** para auditoría o validación de procesos.
- Facilitar la depuración o análisis de eventos recientes.





