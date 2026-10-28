# Base de Datos (PostgreSQL / Supabase)

Estructura de persistencia relacional del sistema:

- `schema/`: Definiciones DDL (tablas de usuarios, médicos, pacientes, horarios, citas, bloqueos temporales, auditoría).
- `seeds/`: Datos semilla de prueba (usuarios de cada rol: admin, médicos verificados/pendientes, pacientes con citas).
- `functions/`: Procedimientos almacenados, triggers, funciones de expiración de turnos (TTL) y cron jobs.
