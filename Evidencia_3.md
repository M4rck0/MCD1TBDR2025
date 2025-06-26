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




# Representación del Diagrama Relacional

```mermaid
erDiagram

  Artist {
    INTEGER ArtistId Llave Primaria
    TEXT Name
  }

  Album {
    INTEGER AlbumId Llave Primaria
    TEXT Title
    INTEGER ArtistId
  }

  Track {
    INTEGER TrackId Llave Primaria
    TEXT Name
    INTEGER AlbumId
    INTEGER MediaTypeId
    INTEGER GenreId
    TEXT Composer
    INTEGER Milliseconds
    INTEGER Bytes
    NUMERIC UnitPrice
  }

  MediaType {
    INTEGER MediaTypeId Llave Primaria
    TEXT Name
  }

  Genre {
    INTEGER GenreId Llave Primaria
    TEXT Name
  }

  Playlist {
    INTEGER PlaylistId Llave Primaria
    TEXT Name
  }

  PlaylistTrack {
    INTEGER PlaylistId
    INTEGER TrackId
  }

  Customer {
    INTEGER CustomerId Llave Primaria
    TEXT FirstName
    TEXT LastName
    TEXT Company
    TEXT Address
    TEXT City
    TEXT State
    TEXT Country
    TEXT PostalCode
    TEXT Phone
    TEXT Fax
    TEXT Email
    INTEGER SupportRepId
  }

  Employee {
    INTEGER EmployeeId Llave Primaria
    TEXT LastName
    TEXT FirstName
    TEXT Title
    INTEGER ReportsTo
    DATE BirthDate
    DATE HireDate
    TEXT Address
    TEXT City
    TEXT State
    TEXT Country
    TEXT PostalCode
    TEXT Phone
    TEXT Fax
    TEXT Email
  }

  Invoice {
    INTEGER InvoiceId Llave Primaria
    INTEGER CustomerId
    DATE InvoiceDate
    TEXT BillingAddress
    TEXT BillingCity
    TEXT BillingState
    TEXT BillingCountry
    TEXT BillingPostalCode
    NUMERIC Total
  }

  InvoiceLine {
    INTEGER InvoiceLineId Llave Primaria
    INTEGER InvoiceId
    INTEGER TrackId
    NUMERIC UnitPrice
    INTEGER Quantity
  }

  Artist ||--o{ Album : produce
  Album ||--o{ Track : contiene
  MediaType ||--o{ Track : usa
  Genre ||--o{ Track : es_de_genero
  Playlist ||--o{ PlaylistTrack : incluye
  Track ||--o{ PlaylistTrack : aparece_en
  Customer ||--o{ Invoice : genera
  Employee ||--o{ Customer : atiende
  Invoice ||--o{ InvoiceLine : tiene
  Track ||--o{ InvoiceLine : vendido_como
  
