# Tarea 2

## 1. Conversión de base de datos a modelo entidad-relación

Se realizó la conversión de la base de datos no estructurada sobre viajes en un modelo entidad-relación. A continuación se presenta el diagrama con las entidades, atributos y relaciones correspondientes, utilizando las figuras adecuadas para cada tipo de nodo:

- **Rectángulo** para la entidad `VIAJE`
- **Elipses** para los atributos simples
- **Números** indicados en las líneas que conectan los nodos

![image](https://github.com/user-attachments/assets/4a5ac5ba-5bae-4b4f-aaa2-8f32c5f03491)

---

## 2. Dominio de los atributos

| Atributo     | Descripción                           | Tipo de dato         | Dominio Ejemplo                           |
|--------------|---------------------------------------|-----------------------|-------------------------------------------|
| START_DATE   | Fecha y hora de inicio del viaje      | datetime              | '2024-05-10 08:30:00'                     |
| END_DATE     | Fecha y hora de fin del viaje         | datetime              | '2024-05-10 09:10:00'                     |
| CATEGORY     | Tipo de viaje                         | string                | {'Business', 'Personal'}                  |
| START        | Lugar donde inicia el viaje           | string                | {'Monterrey', 'CDMX', 'Guadalajara'}     |
| STOP         | Lugar donde termina el viaje          | string                | {'San Pedro', 'CDMX', 'Toluca'}          |
| MILES        | Distancia recorrida en millas         | float o decimal       | Valores positivos, por ejemplo: 3.4, 7.8  |
| PURPOSE      | Propósito del viaje                   | string                | {'Meeting', 'Errand', 'Entertainment'}   |

---

