## Fase 2: Enrutamiento Inter-VLAN, Redundancia L3 (HSRP) y Gestión

- **Objetivo:** Habilitar el enrutamiento entre VLANs en la capa de distribución, implementar redundancia de puerta de enlace mediante **HSRP versión 2** balanceado por VLAN con monitoreo de enlaces ascendentes (*Object Tracking*) y configurar el direccionamiento de gestión en los switches de acceso.
- **Entregables:**
  - Enrutamiento IP (`ip routing`) habilitado e interfaces virtuales (**SVI**) configuradas para las VLANs `10, 20, 30` y `40` en `HQ-CMX-SWC01` y `HQ-CMX-SWC02`.
  - Grupos **HSRPv2** activos con IP virtual `10.1.X.10` y balanceo de carga alineado con Spanning Tree: `HQ-CMX-SWC01` como *Active* en VLANs `10, 40` y `HQ-CMX-SWC02` como *Active* en VLANs `20, 30`.
  - Monitoreo de enlaces ascendentes hacia los routers mediante lista booleana `OR` (`track 10` agrupando `Gi0/1` y `Gi0/2`) con decremento de prioridad (`-20`) y recuperación automática (`preempt`).
  - Interfaces SVI de gestión (`VLAN 10`: `10.1.10.11`–`.13`) y puerta de enlace predeterminada (`10.1.10.10`) configuradas en los switches de acceso (`SWA01`–`SWA03`).
  - Evidencia guardada en `verification/02-validacion-hsrp-tracking.md`.
- **Comandos de validación:** `show standby brief`, `show track brief`, `show spanning-tree vlan <id> | section Root ID`, `ping`

**Conexión Inter-VLAN entre ambos Switches Core**

<details open>
<summary><strong>Switch Core 01</strong></summary>
  
```text
HQ-CMX-SWC01#ping 10.1.10.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.10.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 10/18/28 ms
HQ-CMX-SWC01#ping 10.1.20.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.20.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 11/17/24 ms
HQ-CMX-SWC01#ping 10.1.30.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.30.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 11/17/29 ms
HQ-CMX-SWC01#ping 10.1.40.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.40.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 4/14/19 ms
HQ-CMX-SWC01#
```

<details open>
<summary><strong>Switch Core 02</strong></summary>
  
```text
HQ-CMX-SWC02#ping 10.1.10.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.10.1, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 8/11/13 ms
HQ-CMX-SWC02#ping 10.1.20.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.20.1, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 11/13/15 ms
HQ-CMX-SWC02#ping 10.1.30.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.30.1, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 11/16/25 ms
HQ-CMX-SWC02#ping 10.1.40.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.40.1, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 12/17/25 ms
HQ-CMX-SWC02#
```

**Alineación de HSRP con STP**
<details open>
<summary><strong>Switch Core 01</strong></summary>
  
```text
HQ-CMX-SWC01#show standby brief
                     P indicates configured to preempt.
                     |
Interface   Grp  Pri P State   Active          Standby         Virtual IP
Vl10        10   250 P Active  local           10.1.10.2       10.1.10.10
Vl20        20   240 P Standby 10.1.20.2       local           10.1.20.10
Vl30        30   240 P Standby 10.1.30.2       local           10.1.30.10
Vl40        40   250 P Active  local           10.1.40.2       10.1.40.10
HQ-CMX-SWC01#
HQ-CMX-SWC01#
HQ-CMX-SWC01#show spanning-tree vlan 10 | section Root ID
  Root ID    Priority    10
             Address     0cbd.8f1f.0000
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec


HQ-CMX-SWC01#show spanning-tree vlan 40 | section Root ID
  Root ID    Priority    40
             Address     0cbd.8f1f.0000
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec


HQ-CMX-SWC01#
HQ-CMX-SWC01#show track brief
Track Type        Instance                   Parameter        State Last Change
1     interface   GigabitEthernet0/1         line-protocol    Up    00:12:00
2     interface   GigabitEthernet0/2         line-protocol    Up    00:12:00
10    list                                   boolean          Up    00:11:59
HQ-CMX-SWC01#
```
<details open>
<summary><strong>Switch Core 02</strong></summary>
  
```text
HQ-CMX-SWC02#show standby brief
                     P indicates configured to preempt.
                     |
Interface   Grp  Pri P State   Active          Standby         Virtual IP
Vl10        10   240 P Standby 10.1.10.1       local           10.1.10.10
Vl20        20   250 P Active  local           10.1.20.1       10.1.20.10
Vl30        30   250 P Active  local           10.1.30.1       10.1.30.10
Vl40        40   240 P Standby 10.1.40.1       local           10.1.40.10
HQ-CMX-SWC02#
HQ-CMX-SWC02#
HQ-CMX-SWC02#show spanning-tree vlan 20 | section Root ID
  Root ID    Priority    20
             Address     0c5f.9765.0000
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec


HQ-CMX-SWC02#show spanning-tree vlan 30 | section Root ID
  Root ID    Priority    30
             Address     0c5f.9765.0000
             This bridge is the root
             Hello Time   2 sec  Max Age 20 sec  Forward Delay 15 sec


HQ-CMX-SWC02#
HQ-CMX-SWC02#show track brief
Track Type        Instance                   Parameter        State Last Change
1     interface   GigabitEthernet0/1         line-protocol    Up    00:11:48
2     interface   GigabitEthernet0/2         line-protocol    Up    00:11:48
10    list                                   boolean          Up    00:11:47
HQ-CMX-SWC02#
```
**Conexión de L3 entre Switches de Acceso y Core**
<details open>
<summary><strong>Switch Access 01</strong></summary>
  
```text
HQ-CMX-SWA01#ping 10.1.10.10
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.10.10, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 8/13/26 ms
HQ-CMX-SWA01#
```

<details open>
<summary><strong>Switch Access 02</strong></summary>
  
```text
HQ-CMX-SWA02#ping 10.1.10.10
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.10.10, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 2/207/1016 ms
HQ-CMX-SWA02#
```

<details open>
<summary><strong>Switch Access 03</strong></summary>
  
```text
HQ-CMX-SWA03#ping 10.1.10.10
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.1.10.10, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 5/208/1016 ms
HQ-CMX-SWA03#
```
