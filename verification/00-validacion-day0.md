### Fase 0: Aprovisionamiento Base y Levantamiento de Capa Física (Day-0)

- **Objetivo:** Establecer la convención de nombres, documentar la topología física directamente en cada interfaz mediante descriptions y habilitar los puertos interconectados.
- **Entregables:**
  - Hostnames configurados en los 7 dispositivos de la red.
  - Etiquetado bidireccional de enlaces WAN, Core, Distribución y Acceso.
- **Comando de validación:** `show interfaces description`

<details open>
<summary><strong>Router Core 01</strong></summary>

```text
HQ-CMX-RTR01#show interfaces description
Interface                      Status         Protocol Description
Et0/0                          admin down     down
Gi0/0                          up             up       Link to ISP Router (RTR-ISP01 Gi0/0)
Gi1/0                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi0/1)
Gi2/0                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi0/1)
HQ-CMX-RTR01#
```

<details open>
<summary><strong>Router Core 02</strong></summary>
  
```text
HQ-CMX-RTR02#show interfaces description
Interface                      Status         Protocol Description
Et0/0                          admin down     down
Gi0/0                          up             up       Link to ISP Router (RTR-ISP02 Gi0/0)
Gi1/0                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi0/2)
Gi2/0                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi0/2)
HQ-CMX-RTR02#
```

<details open>
<summary><strong>Switch Core 01</strong></summary>
  
```text
HQ-CMX-SWC01#show interfaces description
Interface                      Status         Protocol Description
Gi0/0                          down           down
Gi0/1                          up             up       Link to Router Core 01 (HQ-CMX-RTR01 Gi1/0)
Gi0/2                          up             up       Link to Router Core 02 (HQ-CMX-RTR02 Gi1/0)
Gi0/3                          down           down
Gi1/0                          down           down
Gi1/1                          up             up       Link to Switch Access 01 (HQ-CMX-SWA01 Gi1/1 - Po1)
Gi1/2                          up             up       Link to Switch Access 01 (HQ-CMX-SWA01 Gi1/2 - Po1)
Gi1/3                          down           down
Gi2/0                          down           down
Gi2/1                          up             up       Link to Switch Access 02 (HQ-CMX-SWA02 Gi1/1 - Po2)
Gi2/2                          up             up       Link to Switch Access 02 (HQ-CMX-SWA02 Gi1/2 - Po2)
Gi2/3                          down           down
Gi3/0                          down           down
Gi3/1                          up             up       Link to Switch Access 03 (HQ-CMX-SWA03 Gi1/1 - Po3)
Gi3/2                          up             up       Link to Switch Access 03 (HQ-CMX-SWA03 Gi1/2 - Po3)
Gi3/3                          down           down
HQ-CMX-SWC01#
```

<details open>
<summary><strong>Switch Core 02</strong></summary>
  
```text
HQ-CMX-SWC02#show interfaces description
Interface                      Status         Protocol Description
Gi0/0                          down           down
Gi0/1                          up             up       Link to Router Core 01 (HQ-CMX-RTR01 Gi2/0)
Gi0/2                          up             up       Link to Router Core 02 (HQ-CMX-RTR02 Gi2/0)
Gi0/3                          down           down
Gi1/0                          down           down
Gi1/1                          up             up       Link to Switch Access 01 (HQ-CMX-SWA01 Gi2/1 - Po4)
Gi1/2                          up             up       Link to Switch Access 01 (HQ-CMX-SWA01 Gi2/2 - Po4)
Gi1/3                          down           down
Gi2/0                          down           down
Gi2/1                          up             up       Link to Switch Access 02 (HQ-CMX-SWA02 Gi2/1 - Po5)
Gi2/2                          up             up       Link to Switch Access 02 (HQ-CMX-SWA02 Gi2/2 - Po5)
Gi2/3                          down           down
Gi3/0                          down           down
Gi3/1                          up             up       Link to Switch Access 03 (HQ-CMX-SWA03 Gi2/1 - Po6)
Gi3/2                          up             up       Link to Switch Access 03 (HQ-CMX-SWA03 Gi2/2 - Po6)
Gi3/3                          down           down
HQ-CMX-SWC02#
```

<details open>
<summary><strong>Switch Access 01</strong></summary>
  
```text
HQ-CMX-SWA01#show interfaces description
Interface                      Status         Protocol Description
Gi0/0                          down           down     Link to PC in VLAN 10 (HQ-CMX-SWA01-PCV10)
Gi0/1                          down           down     Link to PC in VLAN 20 (HQ-CMX-SWA01-PCV20)
Gi0/2                          down           down     Link to PC in VLAN 30 (HQ-CMX-SWA01-PCV30)
Gi0/3                          down           down     Link to PC in VLAN 40 (HQ-CMX-SWA01-PCV40)
Gi1/0                          down           down
Gi1/1                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi1/1 - Po1)
Gi1/2                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi1/2 - Po1)
Gi1/3                          down           down
Gi2/0                          down           down
Gi2/1                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi1/1 - Po4)
Gi2/2                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi1/2 - Po4)
Gi2/3                          down           down
Gi3/0                          down           down
Gi3/1                          down           down
Gi3/2                          down           down
Gi3/3                          down           down
HQ-CMX-SWA01#
```

<details open>
<summary><strong>Switch Access 02</strong></summary>
  
```text
HQ-CMX-SWA02#show interfaces description
Interface                      Status         Protocol Description
Gi0/0                          down           down     Link to PC in VLAN 10 (HQ-CMX-SWA02-PCV10)
Gi0/1                          down           down     Link to PC in VLAN 20 (HQ-CMX-SWA02-PCV20)
Gi0/2                          down           down     Link to PC in VLAN 30 (HQ-CMX-SWA02-PCV30)
Gi0/3                          down           down     Link to PC in VLAN 40 (HQ-CMX-SWA02-PCV40)
Gi1/0                          down           down
Gi1/1                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi2/1 - Po2)
Gi1/2                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi2/2 - Po2)
Gi1/3                          down           down
Gi2/0                          down           down
Gi2/1                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi2/1 - Po5)
Gi2/2                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi2/2 - Po5)
Gi2/3                          down           down
Gi3/0                          down           down
Gi3/1                          down           down
Gi3/2                          down           down
Gi3/3                          down           down
HQ-CMX-SWA02#
```

<details open>
<summary><strong>Switch Access 03</strong></summary>
  
```text
HQ-CMX-SWA03#show interfaces description
Interface                      Status         Protocol Description
Gi0/0                          down           down     Link to PC in VLAN 10 (HQ-CMX-SWA03-PCV10)
Gi0/1                          down           down     Link to PC in VLAN 20 (HQ-CMX-SWA03-PCV20)
Gi0/2                          down           down     Link to PC in VLAN 30 (HQ-CMX-SWA03-PCV30)
Gi0/3                          down           down     Link to PC in VLAN 40 (HQ-CMX-SWA03-PCV40)
Gi1/0                          down           down
Gi1/1                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi3/1 - Po3)
Gi1/2                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi3/2 - Po3)
Gi1/3                          down           down
Gi2/0                          down           down
Gi2/1                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi3/1 - Po6)
Gi2/2                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi3/2 - Po6)
Gi2/3                          down           down
Gi3/0                          down           down
Gi3/1                          down           down
Gi3/2                          down           down
Gi3/3                          down           down
HQ-CMX-SWA03#
```
