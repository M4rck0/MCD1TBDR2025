# 📝 Tarea 8 — Base de Datos Chinook (MySQL)

---

## Vistas (VIEW) con diferentes tipos de JOIN y subconsultas

### 🔹 1. Vista con `JOIN` (INNER JOIN)
```sql
CREATE VIEW Vista_Join AS
SELECT a.AlbumId, a.Title AS AlbumTitle, ar.Name AS ArtistName
FROM Album a
JOIN Artist ar ON a.ArtistId = ar.ArtistId;

