# Enterprise Network

![topology.drawio](https://markdownviewer.pages.dev/api/image/vAqn6tO9zFbq25Xlvbpqbyki)

## Descripción del Proyecto
El presente proyecto comprende el diseño, configuración lógica y validación de una infraestructura de red corporativa bajo una **arquitectura jerárquica redundante de tres capas funcionales**: borde (WAN), núcleo/distribución (Core) y acceso.

La solución integra **7 dispositivos activos** interconectados mediante **enlaces punto a punto** (*dual-homed*) que eliminan los puntos únicos de falla y garantizan la continuidad operativa ante caídas de enlaces o equipos centrales.

> **Plataforma:** GNS3

---

## Objetivo General
Diseñar, implementar y validar una infraestructura de red corporativa bajo una arquitectura jerárquica *High Availability*, compuesta por:
* Capa de borde (Edge)
* Capa distribución (Core)
* Capa de acceso (Access)

Garantizando continuidad operativa, tolerancia a fallos, rendimiento óptimo y seguridad en las comunicaciones de la organización.

## Objetivos Específicos
* **Eliminar puntos únicos de falla** mediante una topología físicamente redundante (*dual-homed*) que interconecta de forma cruzada routers de borde, switches de core/distribución y switches de acceso.
* **Incrementar el ancho de banda y la resiliencia** de los enlaces ascendentes (*uplinks*) mediante agregación de enlaces (**LACP / EtherChannel**) en las conexiones paralelas entre acceso y core.
* **Garantizar la conmutación automática (*failover*) y convergencia sin bucles** en Capa 2 y Capa 3 mediante **RSTP**, **HSRP**, **OSPF (ECMP)** y detección acelerada de fallos con **BFD**.
* **Segmentar lógicamente el tráfico** mediante **VLANs** y aplicar controles de seguridad de primer salto y endurecimiento (*hardening*) para proteger el plano de control y la integridad de los datos.
* **Validar la estabilidad y recuperación ante fallos** mediante pruebas controladas de desconexión y convergencia, documentando la topología y el plan de direccionamiento para su operación y escalabilidad futura.

---

## Capacidades Técnicas Implementadas

### 1. Infraestructura y Convergencia de Capa 2
* **VLANs:** Segmentación lógica por perfiles de tráfico (Datos, Voz, Gestión y Servicios).
* **LACP (IEEE 802.3ad) / EtherChannel:** Agregación de enlaces paralelos entre acceso y núcleo.
* **RSTP (802.1w):** Prevención de bucles, definición de *Root Bridge* primario/secundario, *PortFast* y *BPDU Guard*.

### 2. Redundancia y Enrutamiento de Capa 3
* **Alineación Capa 2 / Capa 3:** Simetría entre el *Root Bridge* de RSTP y el *Gateway* activo de cada VLAN.
* **FHRP (HSRP):** Redundancia de puerta de enlace predeterminada mediante IP/MAC virtual.
* **OSPF (con ECMP):** Enrutamiento dinámico con balanceo de carga de igual costo entre núcleo y borde.
* **BFD (Bidirectional Forwarding Detection):** Detección de fallos en milisegundos vinculada a OSPF y HSRP.
* **Object Tracking:** Supervisión de interfaces ascendentes para conmutación automática ante caídas parciales.

### 3. Seguridad de Primer Salto y Control de Acceso
* **Deshabilitación de puertos sin uso:** Apagado administrativo y aislamiento en VLAN dedicada.
* **Port-Security:** Restricción de direcciones MAC por puerto de acceso.
* **DHCP Snooping:** Bloqueo de servidores DHCP no autorizados y generación de *binding table*.
* **Dynamic ARP Inspection (DAI):** Mitigación de ataques *ARP Spoofing / Man-in-the-Middle*.
* **IP Source Guard (IPSG):** Prevención de suplantación de direcciones IP en puertos de usuario.
* **ACLs:** Filtrado de tráfico Inter-VLAN, control perimetral y restricción hacia la red de gestión.

### 4. Protección del Plano de Control y Gestión
* **Autenticación de protocolos de red:** Cifrado de adyacencias OSPF y mensajes HSRP.
* **Control Plane Policing (CoPP):** Limitación de tasa de tráfico hacia la CPU de routers Edge y switches Core.
* **SSHv2:** Administración remota cifrada con deshabilitación de Telnet/HTTP.
* **NTP autenticado:** Sincronización horaria confiable entre todos los nodos.
* **Syslog:** Centralización de registros y auditoría de eventos.

---

## Estructura del Repositorio
* `/configs` – Archivos de configuración.
* `/docs` – Plan de direccionamiento IP, matriz de VLANs y resultados de pruebas de *failover*.
* `/verification` – Resultados de pruebas de *failover*.