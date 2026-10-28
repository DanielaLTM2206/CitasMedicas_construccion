# Simulador de Concurrencia y Bloqueo Preventivo (RF-015)

- **RF-015**: Bloqueo temporal preventivo (reserva en espera) de 5 minutos (TTL) al seleccionar un turno médico libre.
- **Transaccionalidad**: El turno se oculta en tiempo real para otros pacientes para impedir dobles reservas o colisiones horarias.
- **Expiración y liberación**: Si expira el temporizador de 5 minutos o el paciente abandona la pantalla sin confirmar, el turno se libera de inmediato de forma atómica.
- **Simulador visual**: Vista interactiva en paralelo (Paciente A vs. Paciente B) demostrando el comportamiento del lock en milisegundos.
