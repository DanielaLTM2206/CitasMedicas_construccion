# Capa de Servicios y Estado

- `storage.js`: Administrador de persistencia (integración Supabase Client / LocalStorage mock transaccional con eventos sincronizados).
- `authService.js`: Lógica de autenticación, verificación de tokens temporales de 15 minutos, hashing seguro y control RBAC.
- `appointmentService.js`: Motor de citas, validación de cruces de horario, reglas de antelación mínima y cambios de estado.
- `concurrencyService.js`: Mecanismo de lock preventivo con TTL de 5 minutos y eventos de liberación atómica.
- `emailService.js`: Compilador de plantillas de correo y despachador asíncrono (Resend API / SMTP simulated queue).
- `aiService.js`: Orquestador de intents de lenguaje natural y ejecución de tools para el reagendamiento conversacional.
