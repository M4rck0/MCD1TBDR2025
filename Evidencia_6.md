
# Funciones de Agregación en SQL

## Conteo de Frecuencia

**Objetivo:** Contar cuántas canciones fueron compuestas por alguien cuyo nombre contiene “Brian”.

### Consulta SQL:
```sql
SELECT 
  COUNT(*) AS numero_canciones
FROM 
  Track
WHERE 
  Composer LIKE '%Brian%';
```

```markdown
Resultado:
```
57

## Mínimos o Máximos

**Objetivo:** Obtener la duración mínima y máxima de todas las canciones registradas en la tabla `Track`.

### Consulta SQL:
```sql
SELECT 
  MIN(Milliseconds) AS duracion_minima,
  MAX(Milliseconds) AS duracion_maxima
FROM 
  Track;
```

```markdown
Resultado:
```
duracion_minima | duracion_maxima
----------------|-----------------
1071            | 5286953






## Cuantil cuyo resultado sea distinto a la mediana (Primer Cuartil – Q1)

**Objetivo:** Calcular el primer cuartil (Q1) de la duración de las canciones (`Milliseconds`) en la tabla `Track`, utilizando SQLite y únicamente las funciones y comandos vistos en clase.

### Paso 1: Contar cuántas canciones hay en total

```sql
SELECT COUNT(*) FROM Track;
```

```markdown
Resultado:
```
3503

### Paso 2: Calcular la posición del cuartil
Para encontrar el primer cuartil (Q1), se calcula el 25% del total de datos ordenados de menor a mayor.
En este caso:

$$
Q1 = \text{FLOOR}(3503 \times 0.25) = \text{FLOOR}(875.75) = 875
$$

Al usar OFFSET, la posición se cuenta desde 0, así que:

$$
\text{OFFSET} = 875 - 1 = 874
$$

Esto significa que la fila número 875 representa el primer cuartil, y se accede a ella con OFFSET 874.


```sql
SELECT Name, Milliseconds
FROM Track
ORDER BY Milliseconds
LIMIT 1 OFFSET 874;
```

```markdown
Resultado:
```
Espere Por Mim, Morena | 207072








## Moda 

**Objetivo:** Encontrar el artista que tiene más álbumes registrados (es decir, la moda de `ArtistId` en la tabla `Album`).

### Consulta SQL:
```sql
SELECT Composer, COUNT(*) AS cantidad
FROM Track
WHERE Composer IS NOT NULL
GROUP BY Composer
ORDER BY cantidad DESC
LIMIT 1;
```

```markdown
Resultado:
```
Composer       | cantidad
---------------|---------
Steve Harris   | 80



