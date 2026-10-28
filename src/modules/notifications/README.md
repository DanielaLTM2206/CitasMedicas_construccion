# Módulo de Notificaciones y Recordatorios (RF-010)

- **RF-010**: Generación y despacho de notificaciones transaccionales vía correo electrónico (protocolo SMTP / Resend):
  - Confirmación de agendamiento con detalles (dirección física o enlace virtual de Zoom/Meet).
  - Confirmación de cancelación con motivo registrado.
  - Alerta de reagendamiento exitoso.
  - Recordatorios automáticos enviados 24 horas antes de la cita programada mediante cron job en segundo plano.
- **Simulador de Inbox y Plantillas**: Vista de renderizado de plantillas HTML y simulación de ejecución de tareas programadas (Cron).
