# Subconjunto de Base Chinook

## 1. Crear base de datos

```sql
CREATE DATABASE chinook;
USE chinook;

CREATE TABLE Artist (
  ArtistId INTEGER PRIMARY KEY AUTO_INCREMENT,
  Name TEXT
);

CREATE TABLE Album (
  AlbumId INTEGER PRIMARY KEY AUTO_INCREMENT,
  Title TEXT,
  ArtistId INTEGER,
  FOREIGN KEY (ArtistId) REFERENCES Artist(ArtistId)
);

CREATE TABLE Genre (
  GenreId INTEGER PRIMARY KEY AUTO_INCREMENT,
  Name TEXT
);

CREATE TABLE MediaType (
  MediaTypeId INTEGER PRIMARY KEY AUTO_INCREMENT,
  Name TEXT
);

CREATE TABLE Track (
  TrackId INTEGER PRIMARY KEY AUTO_INCREMENT,
  Name TEXT,
  AlbumId INTEGER,
  MediaTypeId INTEGER,
  GenreId INTEGER,
  Composer TEXT,
  Milliseconds INTEGER,
  Bytes INTEGER,
  UnitPrice NUMERIC,
  FOREIGN KEY (AlbumId) REFERENCES Album(AlbumId),
  FOREIGN KEY (MediaTypeId) REFERENCES MediaType(MediaTypeId),
  FOREIGN KEY (GenreId) REFERENCES Genre(GenreId)
);


-- Artistas
INSERT INTO Artist (Name) VALUES
  ('The Beatles'), ('Pink Floyd'), ('Queen'), ('Led Zeppelin'), ('Radiohead'),
  ('Coldplay'), ('The Rolling Stones'), ('U2'), ('David Bowie'), ('Nirvana');

-- Álbumes
INSERT INTO Album (Title, ArtistId) VALUES
  ('Abbey Road', 1),
  ('The Dark Side of the Moon', 2),
  ('A Night at the Opera', 3),
  ('Led Zeppelin IV', 4),
  ('OK Computer', 5),
  ('Parachutes', 6),
  ('Sticky Fingers', 7),
  ('The Joshua Tree', 8),
  ('Heroes', 9),
  ('Nevermind', 10);

-- Géneros
INSERT INTO Genre (Name) VALUES
  ('Rock'), ('Psychedelic Rock'), ('Alternative'), ('Pop Rock'), ('Hard Rock'),
  ('Grunge'), ('Classic Rock'), ('Electronic'), ('Indie'), ('Britpop');

-- Tipos de Medio
INSERT INTO MediaType (Name) VALUES
  ('MP3'), ('WAV'), ('FLAC'), ('AAC'), ('OGG'),
  ('AIFF'), ('ALAC'), ('DSD'), ('MIDI'), ('WMA');

-- Canciones
INSERT INTO Track (Name, AlbumId, MediaTypeId, GenreId, Composer, Milliseconds, Bytes, UnitPrice) VALUES
  ('Come Together', 1, 1, 1, 'Lennon/McCartney', 259000, 5000000, 0.99),
  ('Time', 2, 2, 2, 'Roger Waters', 413000, 6000000, 1.29),
  ('Bohemian Rhapsody', 3, 3, 1, 'Freddie Mercury', 354000, 5800000, 1.49),
  ('Stairway to Heaven', 4, 4, 5, 'Page/Plant', 482000, 6200000, 1.39),
  ('Karma Police', 5, 1, 3, 'Thom Yorke', 270000, 4800000, 1.19),
  ('Yellow', 6, 5, 4, 'Chris Martin', 270000, 4700000, 0.99),
  ('Brown Sugar', 7, 6, 7, 'Mick Jagger', 250000, 4600000, 1.09),
  ('With or Without You', 8, 7, 1, 'Bono', 295000, 4900000, 1.29),
  ('Heroes', 9, 8, 8, 'David Bowie', 280000, 4500000, 1.19),
  ('Smells Like Teen Spirit', 10, 9, 6, 'Kurt Cobain', 301000, 5500000, 1.49);
