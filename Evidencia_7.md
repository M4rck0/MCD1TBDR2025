# Tarea 7 - Limpieza y Subconsultas en Base de Datos

## 1. Revisión de inconsistencias

Se identificaron registros en la tabla `Customer` donde el campo `State` estaba vacío (`NULL` o cadena vacía). Esto puede causar problemas en análisis.

```sql
SELECT CustomerId, FirstName, LastName, Country, State
FROM Customer
WHERE State IS NULL OR State = '';
```

## 2. Modificaciones o ajustes

### a) Relleno de valores vacíos en `State`

Se decidió asignar el valor `'Sin Estado'` para hacer explícita la falta de información:

```sql
UPDATE Customer
SET State = 'Sin Estado'
WHERE State IS NULL OR State = '';
```

### b) Corrección de códigos postales incompletos

Se identificaron códigos postales con menos de 5 caracteres (Estados Unidos):

```sql
SELECT PostalCode, LENGTH(PostalCode) AS longitud
FROM Customer
WHERE LENGTH(PostalCode) < 5;
```

Y se corrigieron rellenando con ceros a la izquierda:

```sql
UPDATE Customer
SET PostalCode = substr('00000' || PostalCode, -5, 5)
WHERE length(PostalCode) < 5;
```

Además, con `PRAGMA table_info(Customer);` se verificó que la columna `PostalCode` es de tipo `NVARCHAR(10)`, por lo que es correcto tratarla como texto.

---

## 3. Subconsultas relevantes

### a) Clientes que han comprado más de 10 canciones

```sql
SELECT CustomerId, FirstName, LastName
FROM Customer
WHERE CustomerId IN (
  SELECT Invoice.CustomerId
  FROM Invoice
  JOIN InvoiceLine ON Invoice.InvoiceId = InvoiceLine.InvoiceId
  GROUP BY Invoice.CustomerId
  HAVING COUNT(InvoiceLine.TrackId) > 10
);
```

**Ejemplo de resultados (primeros 5):**
- Luís Gonçalves
- Leonie Köhler
- François Tremblay
- Bjørn Hansen
- František Wichterlová

---

### b) Conteo de clientes por país

```sql
SELECT Country, 
       (SELECT COUNT(*) 
        FROM Customer AS c2 
        WHERE c2.Country = c1.Country) AS total_clientes
FROM Customer AS c1
GROUP BY Country;
```

**Ejemplo de resultados (primeros 5):**

| Country    | total_clientes |
|------------|----------------|
| Argentina  | 1              |
| Australia  | 1              |
| Austria    | 1              |
| Belgium    | 1              |
| Brazil     | 5              |

---

## 4. Conclusión

Se realizaron acciones para mejorar la consistencia de los datos, tales como:
- Relleno de valores faltantes,
- Corrección de formatos,
- Aplicación de subconsultas para obtener información relevante de clientes.

