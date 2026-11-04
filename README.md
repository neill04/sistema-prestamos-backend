# Sistema de Préstamos EPCC — Backend

API REST del sistema de préstamo y reserva de equipos, libros y objetos de la EPCC (UNSA). Proyecto universitario.

**Stack:** Java 21, Spring Boot 3.5, Spring Data JPA, PostgreSQL 16, Flyway, Spring Security + JWT, MapStruct, Lombok, springdoc-openapi. Pruebas con JUnit 5, MockMvc y Testcontainers.

## Avance: módulos M0 a M5

| Módulo | Contenido |
|---|---|
| M0 | Base del proyecto: perfiles `dev`/`test`/`prod`, Flyway, errores `ProblemDetail`, CORS, Swagger |
| M1 | Usuarios, roles (estudiante, docente, administrativo, encargado, admin), login con JWT, perfil |
| M2 | Inventario: categorías (plazo y garantía) e ítems con estado |
| M3 | Sanciones por atraso y por daño, y políticas editables |
| M4 | Préstamos: entrega y devolución, garantías, estado físico, atraso y daño |
| M5 | Reservas por rango horario con restricción de exclusión en PostgreSQL (sin solapes), expiración a los 30 min y disponibilidad por ítem |

Pendiente: M6 (historial y vencidos).

## Cómo ejecutarlo

```bash
docker compose up -d                  # PostgreSQL (puerto 5440); el compose está en el repo raíz del proyecto
./mvnw spring-boot:run                # API en :8080 (SERVER_PORT=8095 para otro puerto)
./mvnw verify                         # compila y corre las 206 pruebas (requiere Docker activo)
```

- Swagger UI: `http://localhost:8080/swagger-ui`
- En `dev` se crea un ADMIN de pruebas (`admin@epcc.unsa.edu.pe`, ver `application-dev.yml`).
- En `prod` son obligatorias las variables `JWT_SECRET`, `DB_*` y `CORS_ALLOWED_ORIGINS`.

## Estructura

Paquetes por funcionalidad en `edu.unsa.epcc.loans`: `common`, `auth`, `user`, `inventory`, `sanction`, `loan`, `reservation`. Cada uno con `controller`, `dto`, `entity`, `mapper`, `repository` y `service`. Las migraciones están en `src/main/resources/db/migration` (V1–V7).
