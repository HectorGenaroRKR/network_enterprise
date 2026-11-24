### Fase 0: Aprovisionamiento Base y Levantamiento de Capa Física (Day-0)

- **Objetivo:** Establecer la convención de nombres, documentar la topología física directamente en cada interfaz mediante descriptions y habilitar los puertos interconectados.
- **Entregables:**
  - Hostnames configurados en los 7 dispositivos de la red.
  - Etiquetado bidireccional de enlaces WAN, Core, Distribución y Acceso.
- **Comando de validación:** `show interfaces description`

<details open>
<summary><strong>Router Core 01 (HQ-CMX-RTR01)</strong></summary>

```text
HQ-CMX-RTR01#show interfaces description
Interface                      Status         Protocol Description
Et0/0                          admin down     down
Gi0/0                          up             up       Link to ISP Router (RTR-ISP01 Gi0/0)
Gi1/0                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi0/1)
Gi2/0                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi0/1)
HQ-CMX-RTR01#
