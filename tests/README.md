# Batería de Pruebas de Software

Estructura de pruebas para asegurar la calidad de la solución (Sprint 7 y entregables técnicos):

- `unit/`: Pruebas unitarias de algoritmos de generación de intervalos horarios, validación de contraseñas, hashing y expiración de tokens.
- `concurrency/`: Pruebas de estrés y condición de carrera (race conditions) simulando solicitudes concurrentes al mismo turno médico.
- `e2e/`: Pruebas integrales de flujo de usuario (registro -> validación -> agendamiento -> recordatorio -> reagendamiento con IA -> asistencia médica).
