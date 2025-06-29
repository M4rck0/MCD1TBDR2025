## Esquema de Datos Ficticios (Mockaroo)

Se generaron 100 registros con la siguiente estructura:

| Campo             | Tipo de Dato     | Descripción                      |
|-------------------|------------------|----------------------------------|
| id                | Entero           | Identificador único              |
| nombre            | Texto            | Nombre de persona                |
| apellido_paterno  | Texto            | Apellido paterno                 |
| apellido_materno  | Texto            | Apellido materno                 |
| correo            | Email            | Dirección de correo              |
| genero            | Texto            | Género                           |
| banco             | Texto            | Nombre de banco                  |
| carro             | Texto            | Marca de automóvil               |
| monto             | Dinero ($0–1,000,000) | Simula ingresos             |

Los datos fueron generados automáticamente en [Mockaroo](https://mockaroo.com/) y exportados en formato `.csv`.

## Hallazgos, dificultades y recomendaciones

### Hallazgos
- Mockaroo permite exportar en múltiples formatos útiles: `.csv`, `.json`, `.sql`, `.xlsx`, `.xml`, etc.
- Tiene más de 210 tipos de datos predefinidos, aunque algunos están separados por género (ej. `Male Name`, `Female Name`).
- Si quieres combinar nombres de hombre y mujer en una sola columna, **no hay un tipo genérico llamado solo `Full Name` que mezcle ambos géneros aleatoriamente**.
- Para lograr un "nombre completo", se puede usar una columna combinada (`First Name` + `Last Name`), pero igualmente no se controla el género del nombre.

### Dificultades
- No es posible generar una sola columna de `nombre` que mezcle automáticamente nombres masculinos y femeninos sin dividirlos.
- Si se requiere una columna unificada con nombres completos y variados por género, se debe usar una fórmula personalizada o aceptar la mezcla en campos separados.
- El campo `Money` puede exportarse en $.

### Recomendaciones
- Si necesitas controlar género y nombre, usa `Gender` junto con `First Name` y `Last Name`, y luego combínalos fuera de Mockaroo.
- Usa exportación `.CSV` si tu objetivo es cargar los datos fácilmente en R, Python o Excel.
- Usa exportación `.SQL` si deseas insertar directamente en MySQL o PostgreSQL, pero revisa que los tipos de datos sean compatibles con tu esquema.
- El campo `Money` permite elegir entre distintas monedas: dólar ($), libra (£), euro (€) y yen (¥), lo cual es útil si deseas simular datos internacionales.

