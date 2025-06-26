# Esquema del Modelo Relacional 

## Tabla: Artist
| Columna   | Tipo     | Clave     |
|-----------|----------|-----------|
| ArtistId  | INTEGER  | PRIMARY KEY |
| Name      | TEXT     |           |

---

## Tabla: Album
| Columna   | Tipo     | Clave     |
|-----------|----------|-----------|
| AlbumId   | INTEGER  | PRIMARY KEY |
| Title     | TEXT     |           |
| ArtistId  | INTEGER  |           |

---

## Tabla: Track
| Columna     | Tipo     | Clave     |
|-------------|----------|-----------|
| TrackId     | INTEGER  | PRIMARY KEY |
| Name        | TEXT     |           |
| AlbumId     | INTEGER  |           |
| MediaTypeId | INTEGER  |           |
| GenreId     | INTEGER  |           |
| Composer    | TEXT     |           |
| Milliseconds| INTEGER  |           |
| Bytes       | INTEGER  |           |
| UnitPrice   | NUMERIC  |           |

---

## Tabla: MediaType
| Columna     | Tipo     | Clave     |
|-------------|----------|-----------|
| MediaTypeId | INTEGER  | PRIMARY KEY |
| Name        | TEXT     |           |

---

## Tabla: Genre
| Columna | Tipo    | Clave     |
|---------|---------|-----------|
| GenreId | INTEGER | PRIMARY KEY |
| Name    | TEXT    |           |

---

## Tabla: Playlist
| Columna   | Tipo    | Clave     |
|-----------|---------|-----------|
| PlaylistId| INTEGER | PRIMARY KEY |
| Name      | TEXT    |           |

---

## Tabla: PlaylistTrack
| Columna   | Tipo    | Clave     |
|-----------|---------|-----------|
| PlaylistId| INTEGER |           |
| TrackId   | INTEGER |           |

---

## Tabla: Customer
| Columna     | Tipo    | Clave     |
|-------------|---------|-----------|
| CustomerId  | INTEGER | PRIMARY KEY |
| FirstName   | TEXT    |           |
| LastName    | TEXT    |           |
| Company     | TEXT    |           |
| Address     | TEXT    |           |
| City        | TEXT    |           |
| State       | TEXT    |           |
| Country     | TEXT    |           |
| PostalCode  | TEXT    |           |
| Phone       | TEXT    |           |
| Fax         | TEXT    |           |
| Email       | TEXT    |           |
| SupportRepId| INTEGER |           |

---

## Tabla: Employee
| Columna     | Tipo    | Clave     |
|-------------|---------|-----------|
| EmployeeId  | INTEGER | PRIMARY KEY |
| LastName    | TEXT    |           |
| FirstName   | TEXT    |           |
| Title       | TEXT    |           |
| ReportsTo   | INTEGER |           |
| BirthDate   | DATE    |           |
| HireDate    | DATE    |           |
| Address     | TEXT    |           |
| City        | TEXT    |           |
| State       | TEXT    |           |
| Country     | TEXT    |           |
| PostalCode  | TEXT    |           |
| Phone       | TEXT    |           |
| Fax         | TEXT    |           |
| Email       | TEXT    |           |

---

## Tabla: Invoice
| Columna         | Tipo    | Clave     |
|-----------------|---------|-----------|
| InvoiceId       | INTEGER | PRIMARY KEY |
| CustomerId      | INTEGER |           |
| InvoiceDate     | DATE    |           |
| BillingAddress  | TEXT    |           |
| BillingCity     | TEXT    |           |
| BillingState    | TEXT    |           |
| BillingCountry  | TEXT    |           |
| BillingPostalCode| TEXT   |           |
| Total           | NUMERIC |           |

---

## Tabla: InvoiceLine
| Columna     | Tipo    | Clave     |
|-------------|---------|-----------|
| InvoiceLineId | INTEGER | PRIMARY KEY |
| InvoiceId   | INTEGER |           |
| TrackId     | INTEGER |           |
| UnitPrice   | NUMERIC |           |
| Quantity    | INTEGER |           |




# Punto 2 – Representación del Diagrama Relacional

```mermaid
erDiagram

  EQUIPO {
    SERIAL ID_EQUIPO PK
    VARCHAR NOMBRE_EQUIPO
    INTEGER PL
    NUMERIC EDAD
    INTEGER POS
    INTEGER PJ
    INTEGER TITULAR
    INTEGER MINUTOS
  }

  JUGADOR {
    SERIAL ID_JUGADOR PK
    VARCHAR NOMBRE
    VARCHAR PAIS
    VARCHAR POSC
    INTEGER EQUIPO_ID FK
    DATE NACIMIENTO
    INTEGER PJ
    INTEGER TITULAR
    INTEGER MINUTOS
    NUMERIC NOVENTAS
    INTEGER GOLES
    INTEGER ASISTENCIAS
    INTEGER GOLES_MAS_ASIST
    INTEGER PENALES
    INTEGER TARJETAS_AMARILLAS
    INTEGER TARJETAS_ROJAS
  }

  PARTIDO {
    SERIAL ID_PARTIDO PK
    INTEGER SEMANA
    VARCHAR DIA
    DATE FECHA
    TIME HORA
    INTEGER EQUIPO_LOCAL_ID FK
    NUMERIC XG
    INTEGER MARCADOR_LOCAL
    INTEGER EQUIPO_VISITANTE_ID FK
    INTEGER MARCADOR_VISITANTE
    INTEGER ASISTENCIA
    VARCHAR SEDE
    VARCHAR ARBITRO
  }

  EQUIPO ||--o{ JUGADOR : tiene
  EQUIPO ||--o{ PARTIDO : juega_como_local
  EQUIPO ||--o{ PARTIDO : juega_como_visitante
