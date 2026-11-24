### Fase 0: Aprovisionamiento Base y Levantamiento de Capa Física (Day-0)

* **Objetivo:** Establecer la convención de nombres, documentar la topología física directamente en cada interfaz mediante descriptions y habilitar los puertos interconectados.
* **Entregables:**
Hostnames configurados en los 7 dispositivos de la red.
Etiquetado bidireccional de enlaces WAN, Core, Distribución y Acceso.
* **Comando de validación:** show interfaces description



|**Router Core 01**|
|-|
|HQ-CMX-RTR01#show interfaces description<br />Interface                      Status         Protocol Description<br />Et0/0                          admin down     down<br />Gi0/0                          up             up       Link to ISP Router (RTR-ISP01 Gi0/0)<br />Gi1/0                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi0/1)<br />Gi2/0                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi0/1)<br />HQ-CMX-RTR01#|



|**Router Core 02**|
|-|
|HQ-CMX-RTR02#show interfaces description<br />Interface                      Status         Protocol Description<br />Et0/0                          admin down     down<br />Gi0/0                          up             up       Link to ISP Router (RTR-ISP02 Gi0/0)<br />Gi1/0                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi0/2)<br />Gi2/0                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi0/2)<br />HQ-CMX-RTR02#|



|**Switch Core 01**|
|-|
|HQ-CMX-SWC01#show interfaces description<br />Interface                      Status         Protocol Description<br />Gi0/0                          down           down<br />Gi0/1                          up             up       Link to Router Core 01 (HQ-CMX-RTR01 Gi1/0)<br />Gi0/2                          up             up       Link to Router Core 02 (HQ-CMX-RTR02 Gi1/0)<br />Gi0/3                          down           down<br />Gi1/0                          down           down<br />Gi1/1                          up             up       Link to Switch Access 01 (HQ-CMX-SWA01 Gi1/1 - Po1)<br />Gi1/2                          up             up       Link to Switch Access 01 (HQ-CMX-SWA01 Gi1/2 - Po1)<br />Gi1/3                          down           down<br />Gi2/0                          down           down<br />Gi2/1                          up             up       Link to Switch Access 02 (HQ-CMX-SWA02 Gi1/1 - Po2)<br />Gi2/2                          up             up       Link to Switch Access 02 (HQ-CMX-SWA02 Gi1/2 - Po2)<br />Gi2/3                          down           down<br />Gi3/0                          down           down<br />Gi3/1                          up             up       Link to Switch Access 03 (HQ-CMX-SWA03 Gi1/1 - Po3)<br />Gi3/2                          up             up       Link to Switch Access 03 (HQ-CMX-SWA03 Gi1/2 - Po3)<br />Gi3/3                          down           down<br />HQ-CMX-SWC01#|





|**Switch Core 02**|
|-|
|HQ-CMX-SWC02#show interfaces description<br />Interface                      Status         Protocol Description<br />Gi0/0                          down           down<br />Gi0/1                          up             up       Link to Router Core 01 (HQ-CMX-RTR01 Gi2/0)<br />Gi0/2                          up             up       Link to Router Core 02 (HQ-CMX-RTR02 Gi2/0)<br />Gi0/3                          down           down<br />Gi1/0                          down           down<br />Gi1/1                          up             up       Link to Switch Access 01 (HQ-CMX-SWA01 Gi2/1 - Po4)<br />Gi1/2                          up             up       Link to Switch Access 01 (HQ-CMX-SWA01 Gi2/2 - Po4)<br />Gi1/3                          down           down<br />Gi2/0                          down           down<br />Gi2/1                          up             up       Link to Switch Access 02 (HQ-CMX-SWA02 Gi2/1 - Po5)<br />Gi2/2                          up             up       Link to Switch Access 02 (HQ-CMX-SWA02 Gi2/2 - Po5)<br />Gi2/3                          down           down<br />Gi3/0                          down           down<br />Gi3/1                          up             up       Link to Switch Access 03 (HQ-CMX-SWA03 Gi2/1 - Po6)<br />Gi3/2                          up             up       Link to Switch Access 03 (HQ-CMX-SWA03 Gi2/2 - Po6)<br />Gi3/3                          down           down<br />HQ-CMX-SWC02#|





|**Switch Access 01**|
|-|
|HQ-CMX-SWA01#show interfaces description<br />Interface                      Status         Protocol Description<br />Gi0/0                          down           down     Link to PC in VLAN 10 (HQ-CMX-SWA01-PCV10)<br />Gi0/1                          down           down     Link to PC in VLAN 20 (HQ-CMX-SWA01-PCV20)<br />Gi0/2                          down           down     Link to PC in VLAN 30 (HQ-CMX-SWA01-PCV30)<br />Gi0/3                          down           down     Link to PC in VLAN 40 (HQ-CMX-SWA01-PCV40)<br />Gi1/0                          down           down<br />Gi1/1                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi1/1 - Po1)<br />Gi1/2                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi1/2 - Po1)<br />Gi1/3                          down           down<br />Gi2/0                          down           down<br />Gi2/1                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi1/1 - Po4)<br />Gi2/2                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi1/2 - Po4)<br />Gi2/3                          down           down<br />Gi3/0                          down           down<br />Gi3/1                          down           down<br />Gi3/2                          down           down<br />Gi3/3                          down           down<br />HQ-CMX-SWA01#|



|**Switch Access 02**|
|-|
|HQ-CMX-SWA02#show interfaces description<br />Interface                      Status         Protocol Description<br />Gi0/0                          down           down     Link to PC in VLAN 10 (HQ-CMX-SWA02-PCV10)<br />Gi0/1                          down           down     Link to PC in VLAN 20 (HQ-CMX-SWA02-PCV20)<br />Gi0/2                          down           down     Link to PC in VLAN 30 (HQ-CMX-SWA02-PCV30)<br />Gi0/3                          down           down     Link to PC in VLAN 40 (HQ-CMX-SWA02-PCV40)<br />Gi1/0                          down           down<br />Gi1/1                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi2/1 - Po2)<br />Gi1/2                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi2/2 - Po2)<br />Gi1/3                          down           down<br />Gi2/0                          down           down<br />Gi2/1                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi2/1 - Po5)<br />Gi2/2                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi2/2 - Po5)<br />Gi2/3                          down           down<br />Gi3/0                          down           down<br />Gi3/1                          down           down<br />Gi3/2                          down           down<br />Gi3/3                          down           down<br />HQ-CMX-SWA02#|



|**Switch Access 03**|
|-|
|HQ-CMX-SWA03#show interfaces description<br />Interface                      Status         Protocol Description<br />Gi0/0                          down           down     Link to PC in VLAN 10 (HQ-CMX-SWA03-PCV10)<br />Gi0/1                          down           down     Link to PC in VLAN 20 (HQ-CMX-SWA03-PCV20)<br />Gi0/2                          down           down     Link to PC in VLAN 30 (HQ-CMX-SWA03-PCV30)<br />Gi0/3                          down           down     Link to PC in VLAN 40 (HQ-CMX-SWA03-PCV40)<br />Gi1/0                          down           down<br />Gi1/1                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi3/1 - Po3)<br />Gi1/2                          up             up       Link to Switch Core 01 (HQ-CMX-SWC01 Gi3/2 - Po3)<br />Gi1/3                          down           down<br />Gi2/0                          down           down<br />Gi2/1                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi3/1 - Po6)<br />Gi2/2                          up             up       Link to Switch Core 02 (HQ-CMX-SWC02 Gi3/2 - Po6)<br />Gi2/3                          down           down<br />Gi3/0                          down           down<br />Gi3/1                          down           down<br />Gi3/2                          down           down<br />Gi3/3                          down           down<br />HQ-CMX-SWA03#|







