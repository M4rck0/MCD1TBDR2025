# Tarea 1

## Descripción de la base de datos

En una aplicación de transporte, los usuarios solicitan viajes que tienen registrados datos como la fecha y hora de inicio y fin del recorrido, el lugar donde comenzó y terminó el viaje, la distancia en millas y el propósito del mismo. Cada viaje puede estar categorizado como personal o de negocios. Por ejemplo, algunos viajes se realizan para asistir a juntas de trabajo, otros para realizar diligencias o simplemente para entretenerse. Esta información permite analizar patrones de movilidad, duración promedio, motivos más comunes y zonas de mayor tráfico.

## Diccionario de Datos

| Atributo    | Descripción                                         | Tipo de dato       |
|:-----------:|:---------------------------------------------------:|:------------------:|
| START_DATE  | Fecha y hora de inicio del viaje                    | `datetime`         |
| END_DATE    | Fecha y hora de finalización del viaje              | `datetime`         |
| CATEGORY    | Tipo de viaje (ej. "Business", "Personal")          | `texto (string)`   |
| START       | Ciudad o punto de partida                           | `texto (string)`   |
| STOP        | Ciudad o punto de destino                           | `texto (string)`   |
| MILES       | Distancia recorrida en millas                       | `decimal` o `float`|
| PURPOSE     | Motivo del viaje (ej. "Meeting")                    | `texto (string)`   |

## Investigación sobre SGBD

### PostgreSQL

PostgreSQL es un sistema de gestión de bases de datos objeto-relacional de código abierto, distribuido bajo licencia BSD. Se caracteriza por su estabilidad, soporte para transacciones ACID, integridad referencial y funcionalidades avanzadas como replicación sincrónica, autenticación múltiple, acceso encriptado vía SSL y recuperación punto en el tiempo. Está disponible para múltiples sistemas operativos, incluyendo Windows, Linux, Solaris y macOS. Utiliza un modelo cliente/servidor con multiprocesos, lo que permite que si un proceso falla, no afecte al resto del sistema.  
**Referencia:** Ordóñez, M. P. Z., Ríos, J. R. M., & Castillo, F. F. R. (2017). *Administración de Bases de datos con PostgreSQL (Vol. 19)*. 3Ciencias.

### Oracle

Oracle es uno de los principales sistemas de gestión de bases de datos (SGBD) que soporta el modelo relacional. Está diseñado para manejar grandes volúmenes de información y realizar operaciones complejas como inserción, consulta, actualización y borrado (CRUD). Su robustez, control de transacciones (ACID), integridad referencial y escalabilidad lo convierten en una de las herramientas más utilizadas en entornos empresariales. Oracle permite realizar operaciones de reunión (join) de forma eficiente y nativa, lo que lo hace especialmente útil para consultas complejas en bases de datos relacionales.  
**Referencia:** Moreno Arboleda, F. J., Quintero Rendón, J. E., & Rueda Vásquez, R. (2016). *Una comparación de rendimiento entre Oracle y MongoDB*. Ciencia e Ingeniería Neogranadina, 26(1), 109-129.

### MySQL

MySQL es un sistema gestor de bases de datos relacional ampliamente conocido por su simplicidad, velocidad y eficiencia. Es ideal para aplicaciones web y comerciales, y está desarrollado en C/C++. Es multiplataforma, soporta múltiples motores de almacenamiento como MyISAM e InnoDB, y permite conexión a través de TCP/IP y sockets. Aunque históricamente tenía limitaciones (como falta de soporte para transacciones o vistas en versiones antiguas), es altamente estable y ha sido adoptado extensamente en entornos de desarrollo web.  
**Referencia:** Casillas Santillán, L. A., Gibert Ginestà, M., & Pérez Mora, Ó. (s.f.). *Bases de datos en MySQL*. Fundación Universitaria Oberta de Cataluña (FUOC), pp. 7–8.

## Elección del SGBD

Para esta actividad, elegí utilizar **PostgreSQL** como sistema de gestión de bases de datos por su eficiencia, seguridad y compatibilidad multiplataforma. La base de datos que emplearé proviene del repositorio de GitHub [Uber Rides Data Analysis](https://github.com/Geo-y20/Uber-Rides-Data-Analysis), el cual contiene registros de viajes solicitados por usuarios en una aplicación de transporte. Esta información incluye fecha y hora de inicio y fin, ubicaciones de origen y destino, distancia recorrida y propósito del viaje (personal o de negocios), lo que permite realizar análisis sobre patrones de movilidad, tiempos promedio y motivos de viaje más frecuentes.
