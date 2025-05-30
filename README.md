# PostgreSQL: 

PostgreSQL es un sistema de gestión de bases de datos objeto-relacional de código abierto, distribuido bajo licencia BSD. Se caracteriza por su estabilidad, soporte para transacciones ACID, integridad referencial y funcionalidades avanzadas como replicación sincrónica, autenticación múltiple, acceso encriptado vía SSL y recuperación punto en el tiempo. Está disponible para múltiples sistemas operativos, incluyendo Windows, Linux, Solaris y macOS. Utiliza un modelo cliente/servidor con multiprocesos, lo que permite que si un proceso falla, no afecte al resto del sistema (Zea Ordóñez, Molina Ríos y Redrován Castillo, 2017). 

 

Oracle: 

Oracle es uno de los principales sistemas de gestión de bases de datos (SGBD) que soporta el modelo relacional. Está diseñado para manejar grandes volúmenes de información y realizar operaciones complejas como inserción, consulta, actualización y borrado (CRUD). Su robustez, control de transacciones (ACID), integridad referencial y escalabilidad lo convierten en una de las herramientas más utilizadas en entornos empresariales. Oracle permite realizar operaciones de reunión (join) de forma eficiente y nativa, lo que lo hace especialmente útil para consultas complejas en bases de datos relacionales (Moreno Arboleda, Quintero Rendón y Rueda Vásquez, 2016). 

 

MySQL: 

MySQL es un sistema gestor de bases de datos relacional ampliamente conocido por su simplicidad, velocidad y eficiencia. Es ideal para aplicaciones web y comerciales, y está desarrollado en C/C++. Es multiplataforma, soporta múltiples motores de almacenamiento como MyISAM e InnoDB, y permite conexión a través de TCP/IP y sockets. Aunque históricamente tenía limitaciones (como falta de soporte para transacciones o vistas en versiones antiguas), es altamente estable y ha sido adoptado extensamente en entornos de desarrollo web (Casillas Santillán, Gibert Ginestà y Pérez Mora, s.f.). 

 

 

Para esta actividad, elegí utilizar PostgreSQL como sistema de gestión de bases de datos por su eficiencia, seguridad y compatibilidad multiplataforma. La base de datos que emplearé proviene del repositorio de GitHub Uber Rides Data Analysis, el cual contiene registros de viajes solicitados por usuarios en una aplicación de transporte. Esta información incluye fecha y hora de inicio y fin, ubicaciones de origen y destino, distancia recorrida y propósito del viaje (personal o de negocios), lo que permite realizar análisis sobre patrones de movilidad, tiempos promedio y motivos de viaje más frecuentes. 

 

Ordóñez, M. P. Z., Ríos, J. R. M., & Castillo, F. F. R. (2017). Administración de Bases de datos con PostgreSQL (Vol. 19). 3Ciencias. 

Moreno Arboleda, F. J., Quintero Rendón, J. E., & Rueda Vásquez, R. (2016). Una comparación de rendimiento entre Oracle y MongoDB. Ciencia e Ingeniería Neogranadina, 26(1), 109-129. 

Casillas Santillán, L. A., Gibert Ginestà, M., & Pérez Mora, Ó. (s.f.). Bases de datos en MySQL. Fundación Universitaria Oberta de Cataluña (FUOC), pp. 7–8. 
