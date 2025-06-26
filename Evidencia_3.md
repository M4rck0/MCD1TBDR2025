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

Artist(_ArtistId_, Name)

Album(_AlbumId_, Title, ArtistId)

Track(_TrackId_, Name, AlbumId, MediaTypeId, GenreId, Composer, Milliseconds, Bytes, UnitPrice)

MediaType(_MediaTypeId_, Name)

Genre(_GenreId_, Name)

Playlist(_PlaylistId_, Name)

PlaylistTrack(_PlaylistId_, _TrackId_)

Customer(_CustomerId_, FirstName, LastName, Company, Address, City, State, Country, PostalCode, Phone, Fax, Email, SupportRepId)

Employee(_EmployeeId_, LastName, FirstName, Title, ReportsTo, BirthDate, HireDate, Address, City, State, Country, PostalCode, Phone, Fax, Email)

Invoice(_InvoiceId_, CustomerId, InvoiceDate, BillingAddress, BillingCity, BillingState, BillingCountry, BillingPostalCode, Total)

InvoiceLine(_InvoiceLineId_, InvoiceId, TrackId, UnitPrice, Quantity)
