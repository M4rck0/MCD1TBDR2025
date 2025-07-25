# 📝 Tarea 8 — Base de Datos Chinook (MySQL)

**Nombre:** [Tu Nombre]  
**Materia:** Bases de Datos Relacionales  
**Base de Datos:** Chinook (MySQL)  
**Fecha:** [Fecha de entrega]

---

## ✅ Parte 1: Vistas (VIEW) con diferentes tipos de JOIN y subconsultas

### 🔹 1. Vista con `JOIN` (INNER JOIN)
```sql
CREATE VIEW Vista_Join AS
SELECT a.AlbumId, a.Title AS AlbumTitle, ar.Name AS ArtistName
FROM Album a
JOIN Artist ar ON a.ArtistId = ar.ArtistId;
