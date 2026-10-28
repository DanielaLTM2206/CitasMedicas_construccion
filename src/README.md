# Código Fuente del Prototipo Web

Este directorio contiene la implementación interactiva del prototipo para el Sistema de Gestión de Citas Médicas:

- `assets/`: Estilos CSS, scripts utilitarios globales y recursos gráficos/multimedia.
- `components/`: Componentes UI reutilizables (Navbar, Modales de confirmación, Toast de alertas, Temporizador regresivo de turnos).
- `modules/`:
  - `auth/`: Autenticación segura unificada (roles Paciente, Médico, Admin), registro de pacientes en 2 pasos y recuperación de contraseña.
  - `patient/`: Portal del paciente para agendamiento interactivo (presencial y virtual) y cancelación justificada de citas.
  - `doctor/`: Portal médico para parametrización de agenda, generación de bloques de atención, marcación de asistencia en tiempo real y reportes estadísticos.
  - `admin/`: Panel administrativo de auditoría de licencias médicas, baja lógica de cuentas y configuración de políticas del agente IA.
  - `ai-agent/`: Asistente conversacional inteligente (SaludBot) para reagendamiento en lenguaje natural con tool calling y validación de antelación.
  - `concurrency/`: Simulador interactivo de bloqueo concurrente de turnos (Paciente A vs Paciente B) con temporizador TTL de 5 minutos.
  - `notifications/`: Simulador de envío de correos transaccionales y recordatorios automáticos de 24 horas vía Resend/SMTP.
- `services/`: Capa de servicios para persistencia (Supabase / Local Mock), lógica de negocio, motor de reservas y simulador de correo.
