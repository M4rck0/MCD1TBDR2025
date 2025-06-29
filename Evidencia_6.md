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

