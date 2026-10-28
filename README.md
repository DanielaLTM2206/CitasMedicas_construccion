# Sistema de Información Web para Gestión de Citas Médicas de Medicina General (SaludDigital)

[![Universidad de las Fuerzas Armadas ESPE](https://img.shields.io/badge/ESPE-Ingenier%C3%ADa%20de%20Software-darkgreen)](https://www.espe.edu.ec/)
[![Materia](https://img.shields.io/badge/Materia-Construcci%C3%B3n%20y%20Evoluci%C3%B3n%20del%20Software-blue)](#)
[![NRC](https://img.shields.io/badge/NRC-36847-lightgrey)](#)
[![Metodología](https://img.shields.io/badge/Metodolog%C3%ADa-Scrum%20H%C3%ADbrido-orange)](#)

---

## 👥 Equipo de Trabajo

| Integrante | Rol Principal | Responsabilidades |
| :--- | :--- | :--- |
| **Daniela Tituaña** | Analista de Requisitos / Diseñadora UI/UX / Frontend | Levantamiento de especificaciones, diseño de interfaces web responsivas, prototipado interactivo y casos de uso. |
| **Stiven (Gustavo) Molina** | Analista de Requisitos / Arquitecto de Software / Backend | Modelo relacional PostgreSQL, control de concurrencia y locks, mensajería SMTP y lógica del asistente conversacional IA. |

**Docente:** Ing. Mayra Isabel Alvarez Jimenez  
**Período:** Octubre 2026 – Febrero 2027  

---

## 📋 Descripción del Proyecto

Plataforma web responsiva diseñada para optimizar y automatizar la gestión integral de citas médicas en el ámbito de **medicina general** para consultorios independientes. El sistema resuelve las principales ineficiencias de la práctica médica ambulatoria:

1. **Ausentismo de pacientes** mediante recordatorios automáticos enviados por correo electrónico con 24 horas de antelación.
2. **Colisiones de horarios y dobles reservas concurrentes** mediante un motor transaccional con bloqueo preventivo de turnos de 5 minutos (TTL).
3. **Carga administrativa manual** integrando un asistente conversacional con inteligencia artificial (**SaludBot**) para el re-agendamiento autónomo en lenguaje natural bajo políticas estrictas de antelación horaria.

---

## 🎯 Requisitos del Sistema

### Catálogo de Requisitos Funcionales (RF)

| ID | Requisito Funcional | Módulo / Actor | Descripción Resumida |
| :--- | :--- | :--- | :--- |
| **RF-001** | Registro de Paciente y Verificación | Paciente / Autenticación | Registro con validación de cédula, contraseña segura y activación obligatoria por código vía email. |
| **RF-002** | Agendamiento de Citas | Paciente / Citas | Selección de médico, fecha, hora, motivo y modalidad (Presencial en Consultorio o Consulta Virtual). |
| **RF-003** | Auto-Registro de Médico General | Médico / Registro | Solicitud de cuenta médica, datos de consultorio y carga digital de licencia profesional en PDF. |
| **RF-004** | Gestión de Calendario Laboral | Médico / Agenda | Parametrización de días laborables, franjas horarias, duración (20/30 min), buffer y recesos. |
| **RF-005** | Registro de Asistencia a Citas | Médico / Agenda | Marcación en tiempo real del estado final de la consulta: `Atendida` o `Inasistencia` con observaciones. |
| **RF-006** | Auditoría y Aprobación de Médicos | Administrador | Revisión de licencias en PDF, aprobación (`Activo`), solicitud de subsanación o rechazo definitivo. |
| **RF-007** | Reportes Estadísticos de Citas | Médico / Admin | Métricas de rendimiento, tasas de asistencia, filtros por fechas y exportación en formatos PDF/CSV. |
| **RF-008** | Autenticación y Control de Acceso (RBAC) | Todos los Roles | Login seguro con redirección a dashboards según rol; bloqueo estricto a cuentas inactivas/pendientes. |
| **RF-009** | Cancelación de Citas Médicas | Paciente / Médico | Cancelación justificada con motivo obligatorio, validación de tiempo mínimo y liberación inmediata de cupo. |
| **RF-010** | Notificaciones y Recordatorios | Sistema / Correo | Despacho automático de emails transaccionales (creación/cancelación) y recordatorios 24h previas. |
| **RF-011** | Re-agendamiento Asistido por IA | Paciente / IA | Asistente conversacional en lenguaje natural con tool calling para sugerir y confirmar nuevos horarios. |
| **RF-012** | Configuración de Políticas de IA | Admin / Médico | Parametrización de horas mínimas de antelación con las que puede operar el asistente de IA. |
| **RF-013** | Baja Lógica de Cuentas | Administrador | Inactivación de médicos o pacientes sin eliminar historial médico/transaccional, verificando citas futuras. |
| **RF-014** | Recuperación de Contraseña | Autenticación | Restablecimiento de contraseña mediante token temporal de un solo uso con caducidad de 15 min por email. |
| **RF-015** | Bloqueo Preventivo Concurrente | Motor Transaccional | Reserva temporal de 5 minutos sobre un turno en proceso de agendamiento para evitar colisiones. |

### Requisitos No Funcionales (RNF)

- **Rendimiento:** Actualización y visualización de calendarios en menos de 2 segundos. Registro de asistencia y cambios de estado en menos de 1 segundo. Envío de correos transaccionales en menos de 5 segundos.
- **Seguridad:** Cifrado unidireccional de credenciales mediante algoritmos seguros (Argon2id o bcrypt). Control de acceso basado en roles (RBAC). Aislamiento estricto de funciones para el agente de IA.
- **Concurrencia:** Consistencia transaccional inmediata y bloqueo temporal (TTL de 5 min) sin degradar la base de datos.
- **Auditoría:** Persistencia mediante baja lógica para garantizar la trazabilidad de citas previas.

### Restricciones del Proyecto (RES)

1. **RES-01 (Canal de Notificaciones):** Exclusivamente por correo electrónico vía SMTP / Resend API (sin SMS ni WhatsApp).
2. **RES-02 (Especialidad Única):** Restringido exclusivamente al área de Medicina General.
3. **RES-03 (Sin Pagos ni Facturación):** No incluye módulos de cobro transaccional ni facturación electrónica.
4. **RES-04 (Registro Clínico Acotado):** Almacena únicamente motivo inicial y estado de asistencia (sin recetas complejas ni CIE-10).
5. **RES-05 (Plataforma Web Responsiva):** Aplicativo accesible desde navegadores web (escritorio y móviles), descartando apps nativas de tiendas móviles.
6. **RES-06 (Teleconsultas):** Enlaces externos integrados (Zoom / Google Meet), sin servidores propios WebRTC.
7. **RES-07 (Límite del Asistente IA):** Limitado estrictamente a re-agendar citas existentes; no atiende consultas médicas ni agenda turnos desde cero.

---

## 🗂️ Estructura del Repositorio

El repositorio se encuentra organizado de acuerdo con el ciclo de vida de la ingeniería de software y la arquitectura modular del prototipo:

```text
CitasMedicas_construccion/
├── .gitignore                          # Configuración de exclusiones de Git
├── README.md                           # Documento principal del repositorio
│
├── docs/                               # Artefactos y Entregables de Ingeniería de Software
│   ├── README.md                       # Índice y propósito de la documentación
│   ├── srs/                            # Especificación de Requisitos de Software (IEEE 830)
│   ├── bpmn/                           # Modelado de procesos de negocio (Bizagi) y matrices
│   ├── uml/                            # Diagramas de Casos de Uso, plantillas y actividades
│   ├── rtm/                            # Matriz de Trazabilidad de Requisitos
│   └── database/                       # Diagramas Entidad-Relación y diccionario de datos
│
├── database/                           # Persistencia y Scripts SQL (PostgreSQL / Supabase)
│   ├── README.md                       # Guía de persistencia y base de datos
│   ├── schema/                         # DDL de tablas, índices, llaves foráneas y constraints
│   ├── seeds/                          # Datos de prueba iniciales (usuarios, turnos, citas)
│   └── functions/                      # Procedimientos, triggers de concurrencia y cron jobs
│
├── src/                                # Código Fuente del Prototipo Web Interactivo
│   ├── README.md                       # Arquitectura y componentes del prototipo
│   ├── assets/                         # Recursos estáticos
│   │   ├── css/                        # Sistema de diseño, tokens, glassmorphism y temas
│   │   ├── js/                         # Utilidades y controladores transversales
│   │   └── images/                     # Logotipos de marca y recursos multimedia
│   ├── components/                     # Componentes reutilizables (Navbar, Modal, Toast, Timer)
│   ├── modules/                        # Módulos organizados por casos de uso y roles
│   │   ├── auth/                       # RF-001, RF-008, RF-014: Login, Registro, Recuperación
│   │   ├── patient/                    # RF-002, RF-009: Agendamiento, Cancelación, Mis Citas
│   │   ├── doctor/                     # RF-003, RF-004, RF-005, RF-007: Agenda, Asistencia, Reportes
│   │   ├── admin/                      # RF-006, RF-012, RF-013: Auditoría, Bajas, Reglas IA
│   │   ├── ai-agent/                   # RF-011, RF-012: SaludBot (Chat inteligente con Tool Calling)
│   │   ├── concurrency/                # RF-015: Simulador de bloqueo preventivo de 5 min (TTL)
│   │   └── notifications/              # RF-010: Plantillas de correo y simulación de recordatorio 24h
│   └── services/                       # Servicios de estado, Supabase Client, Emailer y Mock Data
│
└── tests/                              # Batería de Pruebas de Software
    ├── README.md                       # Estrategia de pruebas y cobertura
    ├── unit/                           # Pruebas unitarias de algoritmos y validaciones
    ├── concurrency/                    # Pruebas de estrés y condición de carrera en turnos
    └── e2e/                            # Pruebas integrales de flujo de usuario
```

---

## 🚀 Planificación y Cronograma de Sprints (Linear)

| Ciclo | Período | Objetivo y Entregables Clave |
| :--- | :--- | :--- |
| **Sprint 0** | 26 Oct – 08 Nov 2026 | Consolidación de requisitos, modelado BPMN en Bizagi y arquitectura de datos PostgreSQL. |
| **Sprint 1** | 09 Nov – 22 Nov 2026 | Autenticación, control de accesos RBAC y validación de cuentas vía correo. |
| **Sprint 2** | 23 Nov – 06 Dic 2026 | Registro médico con carga de licencias en PDF y panel administrativo de auditoría. |
| **Sprint 3** | 07 Dic – 20 Dic 2026 | Módulo de configuración de jornadas laborales, descansos y publicación de cupos. |
| **Sprint 4** | 21 Dic – 03 Ene 2027 | Motor transaccional de reservas con bloqueo preventivo de 5 minutos y notificaciones SMTP. |
| **Sprint 5** | 04 Ene – 17 Ene 2027 | Integración del asistente conversacional con IA para reprogramación bajo reglas de antelación. |
| **Sprint 6** | 18 Ene – 31 Ene 2027 | Marcación médica de asistencia, exportación de reportes a PDF/Excel y módulo de bajas lógicas. |
| **Sprint 7** | 01 Feb – 14 Feb 2027 | Batería transversal de pruebas de estrés para reservas simultáneas y pruebas E2E. |
| **Cierre** | 15 Feb – 28 Feb 2027 | Despliegue del entorno web, manuales de usuario y sustentación final del proyecto. |