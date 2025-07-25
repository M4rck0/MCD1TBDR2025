# Tarea 9 — Procedimientos y funciones

---

## Correlación entre dos conjuntos de datos

Calcula el coeficiente de correlación de Pearson entre las columnas `x` y `y` de la tabla `datos`, usando la fórmula estadística estándar.

```sql
DELIMITER $$

CREATE PROCEDURE calcular_correlacion(
  OUT correlacion DOUBLE
)
BEGIN
  DECLARE n INT;
  DECLARE sum_x DOUBLE;
  DECLARE sum_y DOUBLE;
  DECLARE sum_xy DOUBLE;
  DECLARE sum_x2 DOUBLE;
  DECLARE sum_y2 DOUBLE;

  SELECT 
    COUNT(*),
    SUM(x),
    SUM(y),
    SUM(x * y),
    SUM(x * x),
    SUM(y * y)
  INTO n, sum_x, sum_y, sum_xy, sum_x2, sum_y2
  FROM datos;

  SET correlacion = (n * sum_xy - sum_x * sum_y) / 
                    (SQRT(n * sum_x2 - POW(sum_x, 2)) * 
                     SQRT(n * sum_y2 - POW(sum_y, 2)));
END $$

DELIMITER ;
```

### Ejemplo

#### Paso 1: Crear tabla

```sql
CREATE TABLE datos (
  x DOUBLE,
  y DOUBLE
);
```

#### Paso 2: Insertar datos

```sql
INSERT INTO datos (x, y) VALUES
(1, 2),
(2, 4),
(3, 6),
(4, 8),
(5, 10);
```

#### Correlación

```sql
SET @r := 0;
CALL calcular_correlacion(@r);
SELECT @r AS correlacion;
```

Resultado: $1$




## Distancia de Levenshtein entre cadenas de caracteres

Esta función calcula la distancia de Levenshtein entre dos cadenas, la cual representa el número mínimo de operaciones (inserciones, eliminaciones o sustituciones) necesarias para transformar una cadena en otra.

```sql
DELIMITER $$

CREATE FUNCTION levenshtein(s1 VARCHAR(255), s2 VARCHAR(255)) 
RETURNS INT DETERMINISTIC
BEGIN
  DECLARE s1_len, s2_len, i, j, cost, lastdiag, olddiag INT;
  DECLARE s1_char CHAR(1);
  DECLARE d0 VARBINARY(256);
  DECLARE d1 VARBINARY(256);

  SET s1_len = CHAR_LENGTH(s1);
  SET s2_len = CHAR_LENGTH(s2);
  SET d0 = REPEAT(CHAR(0), s2_len + 1);
  SET d1 = REPEAT(CHAR(0), s2_len + 1);

  SET j = 0;
  WHILE j <= s2_len DO
    SET d0 = INSERT(d0, j + 1, 1, CHAR(j));
    SET j = j + 1;
  END WHILE;

  SET i = 1;
  WHILE i <= s1_len DO
    SET s1_char = SUBSTRING(s1, i, 1);
    SET d1 = INSERT(d1, 1, 1, CHAR(i));
    SET j = 1;
    WHILE j <= s2_len DO
      SET cost = IF(s1_char = SUBSTRING(s2, j, 1), 0, 1);
      SET d1 = INSERT(d1, j + 1, 1, CHAR(
        LEAST(
          ASCII(SUBSTRING(d1, j, 1)) + 1,
          ASCII(SUBSTRING(d0, j + 1, 1)) + 1,
          ASCII(SUBSTRING(d0, j, 1)) + cost
        )
      ));
      SET j = j + 1;
    END WHILE;
    SET d0 = d1;
    SET i = i + 1;
  END WHILE;

  RETURN ASCII(SUBSTRING(d1, s2_len + 1, 1));
END $$

DELIMITER ;
```

### Ejemplo

```sql
SELECT levenshtein('casa', 'caso');
```

Resultado: $1$





## Cantidad de elementos de un arreglo

Esta función recibe una cadena de texto en la que los elementos están separados por comas (`,`) y devuelve la cantidad total de elementos. Se simula el comportamiento de un arreglo al contar las comas y ajusta el resultado dependiendo de si la cadena está vacía. 

```sql
DELIMITER $$

CREATE FUNCTION contar_elementos(arreglo TEXT)
RETURNS INT DETERMINISTIC
BEGIN
  DECLARE contador INT DEFAULT 1;
  DECLARE i INT DEFAULT 1;

  WHILE LOCATE(',', arreglo, i) > 0 DO
    SET contador = contador + 1;
    SET i = LOCATE(',', arreglo, i) + 1;
  END WHILE;

  RETURN IF(TRIM(arreglo) = '', 0, contador);
END $$

DELIMITER ;
```

### Ejemplo 1

```sql
SELECT contar_elementos('uno,dos,tres,cuatro');
```

Resultado: $4$



### Ejemplo 2

```sql
SELECT contar_elementos('');  
```

Resultado: $0$
