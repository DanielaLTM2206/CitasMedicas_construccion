# Prototipo Interactivo de Software (SaludDigital / Portal SaludPlus)

Este directorio alberga la implementación del **Prototipo Funcional de Software**, diseñado con base en los wireframes y requerimientos del Plan de Construcción (Entregable 3) para la asignatura *Construcción y Evolución del Software* (ESPE).

---

## 📂 Organización del Prototipo

```text
prototipo/
├── README.md                   # Documentación y guía del prototipo
├── index.html                  # Dashboard / Punto de entrada principal interactivo
├── assets/                     # Recursos visuales, iconos y marcas
├── css/                        # Estilos CSS (diseño responsivo, glassmorphism, variables de color)
├── js/                         # Scripts de interactividad, almacenamiento local y simulación
└── views/                      # Pantallas del prototipo organizadas por actor y caso de uso:
    ├── auth/                   # Pantallas de Login (3 roles), Registro en 2 pasos y Recuperación
    ├── paciente/               # Flujos de Agendamiento (presencial/virtual), Mis Citas y Cancelación
    ├── medico/                 # Gestión de Agenda, Control de Asistencia y Reportes Estadísticos
    ├── admin/                  # Auditoría de Licencias PDF, Baja Lógica y Parámetros IA
    └── simuladores/            # Simulador de Concurrencia (Paciente A vs B) y Recordatorios 24h
```

---

## 🖥️ Pantallas Modeladas según Wireframes

1. **Autenticación (RF-001, RF-002, RF-014):**
   - Formulario de Registro de Paciente en 2 pasos con validación de cédula y código de activación.
   - Portal de Login con pestañas para Paciente, Médico y Administrador.
   - Recuperación de contraseña por enlace temporal de 15 minutos.

2. **Portal del Paciente (RF-004, RF-005, RF-006):**
   - Agendamiento de citas con filtro de modalidad (Presencial / Consulta Virtual).
   - Historial de citas con opciones para Cancelar y Re-agendar.
   - Asistente conversacional IA (**SaludBot**) para cambio de turnos en lenguaje natural.

3. **Portal del Médico General (RF-003, RF-004, RF-005, RF-007, RF-010):**
   - Solicitud de registro con subida de título/licencia en PDF.
   - Parametrización de jornada laboral, recesos de almuerzo y buffer entre consultas.
   - Agenda médica del día en tiempo real para marcar `Atendida` o `Inasistencia`.
   - Panel de reportes estadísticos con gráficos de ocupación y exportación PDF/CSV.

4. **Portal del Administrador (RF-006, RF-012, RF-013):**
   - Mesa de auditoría de licencias profesionales para aprobación o veto.
   - Directorio de usuarios para baja lógica motivada.
   - Configuración de reglas de antelación para el asistente conversacional.

5. **Simuladores de Arquitectura Transaccional:**
   - **Simulador de Concurrencia (RF-015):** Demostración en paralelo del bloqueo preventivo de 5 minutos sobre un turno para evitar colisiones.
   - **Simulador de Recordatorios 24h (RF-010):** Vista de despacho de correos automáticos vía SMTP/Resend.
