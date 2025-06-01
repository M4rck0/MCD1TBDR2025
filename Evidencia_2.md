# Tarea 2

## 1. Conversión de base de datos a modelo entidad-relación

Se realizó la conversión de la base de datos no estructurada sobre viajes en un modelo entidad-relación. A continuación se presenta el diagrama con las entidades, atributos y relaciones correspondientes, utilizando las figuras adecuadas para cada tipo de nodo:

- **Rectángulo** para la entidad `VIAJE`
- **Elipses** para los atributos simples
- **Hexágonos** para indicar el dominio de cada atributo
- **Elipse subrayada** para identificar la clave primaria (`START_DATE`)
- **Líneas** que conectan cada atributo con la entidad principal

> En este caso no se utilizaron **rombos** ni **cardinalidades (1:N)** ya que la base de datos describe únicamente una **entidad principal (`VIAJE`)** sin relaciones con otras entidades, por lo que no se requiere representar asociaciones entre múltiples tablas.

<img width="707" alt="Tarea_2_VF" src="https://github.com/user-attachments/assets/19c7aac2-b597-4952-a4c3-c61c699deef4" />


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
