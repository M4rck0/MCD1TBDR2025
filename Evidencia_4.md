# Actividad: Modelo Relacional - Base de Datos Chinook

## 1. Creación de Tablas

```sql
CREATE TABLE Artist (
  ArtistId INT PRIMARY KEY,
  Name VARCHAR(100)
);

CREATE TABLE Album (
  AlbumId INT PRIMARY KEY,
  Title VARCHAR(100),
  ArtistId INT REFERENCES Artist(ArtistId)
);

CREATE TABLE MediaType (
  MediaTypeId INT PRIMARY KEY,
  Name VARCHAR(50)
);

CREATE TABLE Genre (
  GenreId INT PRIMARY KEY,
  Name VARCHAR(50)
);

CREATE TABLE Track (
  TrackId INT PRIMARY KEY,
  Name VARCHAR(100),
  AlbumId INT REFERENCES Album(AlbumId),
  MediaTypeId INT REFERENCES MediaType(MediaTypeId),
  GenreId INT REFERENCES Genre(GenreId),
  Composer VARCHAR(100),
  Milliseconds FLOAT,
  Bytes FLOAT,
  UnitPrice FLOAT
);


-- Tabla Artist
INSERT INTO Artist VALUES
(1, 'AC/DC'),
(2, 'Accept'),
(3, 'Aerosmith'),
(4, 'Alanis Morissette'),
(5, 'Alice In Chains'),
(6, 'Antônio Carlos Jobim'),
(7, 'Apocalyptica'),
(8, 'Audioslave'),
(9, 'BackBeat'),
(10, 'Billy Cobham');

-- Tabla Album
INSERT INTO Album VALUES
(1, 'For Those About To Rock We Salute You', 1),
(2, 'Balls to the Wall', 2),
(3, 'Restless and Wild', 2),
(4, 'Big Ones', 3),
(5, 'Jagged Little Pill', 4),
(6, 'Facelift', 5),
(7, 'Warner 25 Anos', 6),
(8, 'Plays Metallica By Four Cellos', 7),
(9, 'Audioslave', 8),
(10, 'BackBeat Soundtrack', 9);

-- Tabla MediaType
INSERT INTO MediaType VALUES
(1, 'MPEG audio file'),
(2, 'Protected AAC audio file'),
(3, 'Protected MPEG-4 video file'),
(4, 'Purchased AAC audio file'),
(5, 'AAC audio file'),
(6, 'WAV audio file'),
(7, 'FLAC audio file'),
(8, 'OGG audio file'),
(9, 'ALAC audio file'),
(10, 'AIFF audio file');

-- Tabla Genre
INSERT INTO Genre VALUES
(1, 'Rock'),
(2, 'Jazz'),
(3, 'Metal'),
(4, 'Alternative & Punk'),
(5, 'Blues'),
(6, 'Latin'),
(7, 'Reggae'),
(8, 'Classical'),
(9, 'Pop'),
(10, 'Soundtrack');

-- Tabla Track
INSERT INTO Track VALUES
(1, 'For Those About To Rock (We Salute You)', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 343719.0, 11170334.0, 0.99),
(2, 'Balls to the Wall', 2, 2, 3, 'Accept', 342562.0, 5510424.0, 0.99),
(3, 'Fast As a Shark', 3, 1, 3, 'F. Baltes, S. Kaufman, U. Dirkscneider & W. Hoffman', 230619.0, 3990994.0, 0.99),
(4, 'Restless and Wild', 3, 1, 3, 'F. Baltes, R.A. Smith-Diesel, S. Kaufman, U. Dirkscneider', 252051.0, 4331779.0, 0.99),
(5, 'Princess of the Dawn', 3, 1, 3, 'Deaffy & R.A. Smith-Diesel', 375418.0, 6290521.0, 0.99),
(6, 'Put The Finger On You', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 205662.0, 6713451.0, 0.99),
(7, 'Let''s Get It Up', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 233926.0, 7636561.0, 0.99),
(8, 'Inject The Venom', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 210834.0, 6852860.0, 0.99),
(9, 'Snowballed', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 203102.0, 6599424.0, 0.99),
(10, 'Evil Walks', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 263497.0, 8611245.0, 0.99);

