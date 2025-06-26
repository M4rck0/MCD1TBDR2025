# Esquema del Modelo Relacional

## Tabla: EQUIPO
- **ID_Equipo** *(PRIMARY KEY)*
- Nombre_Equipo
- PL
- Edad
- POS
- PJ
- Titular
- Minutos

## Tabla: JUGADOR
- **ID_Jugador** *(PRIMARY KEY)*
- Nombre
- País
- POSC
- Equipo_ID *(FOREIGN KEY → EQUIPO.ID_Equipo)*
- Nacimiento
- PJ
- Titular
- Minutos
- Noventas
- Goles
- Asistencias
- Goles_Mas_Asist
- Penales
- Tarjetas_Amarillas
- Tarjetas_Rojas

## Tabla: PARTIDO
- **ID_Partido** *(PRIMARY KEY)*
- Semana
- Día
- Fecha
- Hora
- Equipo_Local_ID *(FOREIGN KEY → EQUIPO.ID_Equipo)*
- Marcador_Local
- Equipo_Visitante_ID *(FOREIGN KEY → EQUIPO.ID_Equipo)*
- Marcador_Visitante
- Asistencia
- XG
- Sede
- Árbitro
