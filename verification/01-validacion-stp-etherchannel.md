## Fase 1: Conmutación, Segmentación VLAN y Redundancia en L2

- **Objetivo:** Segmentar el tráfico corporativo mediante VLANs `802.1Q`, configurar los enlaces redundantes entre distribución y acceso con **EtherChannel (LACP)** y balancear el plano de control de Capa 2 mediante **Rapid-PVST+**.
- **Entregables:**
  - VLANs `10, 20, 30, 40, 99` y `999` creadas en los 5 switches.
  - Enlaces troncales `802.1Q` seguros (excluyendo `VLAN 1` y asignando `VLAN 99` como nativa).
  - Grupos LACP activos (`Po1`–`Po3` en distribución; `Po1`–`Po2` en acceso).
  - Balanceo de *Root Bridge*: `HQ-CMX-SWC01` (VLANs `10, 40`) y `HQ-CMX-SWC02` (VLANs `20, 30`).
  - Evidencia guardada en `verification/01-validacion-stp-etherchannel.md`.
- **Comandos de validación:** `show vlan brief`, `show etherchannel summary`, `show spanning-tree root`

<details open>
<summary><strong>Switch Core 01</strong></summary>
  
```text
HQ-CMX-SWC01#show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Gi0/0, Gi0/1, Gi0/2, Gi0/3
                                                Gi1/0, Gi1/3, Gi2/0, Gi2/3
                                                Gi3/0, Gi3/3
10   MANAGEMENT                       active
20   USERS                            active
30   VoIP                             active
40   SERVERS                          active
99   NATIVE                           active
999  BLACKHOLE                        active
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
HQ-CMX-SWC01#
HQ-CMX-SWC01#
HQ-CMX-SWC01#
HQ-CMX-SWC01#show etherchannel summary
Flags:  D - down        P - bundled in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      N - not in use, no aggregation
        f - failed to allocate aggregator

Number of channel-groups in use: 3
Number of aggregators:           3

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Gi1/1(P)    Gi1/2(P)
2      Po2(SU)         LACP      Gi2/1(P)    Gi2/2(P)
3      Po3(SU)         LACP      Gi3/1(P)    Gi3/2(P)

HQ-CMX-SWC01#
HQ-CMX-SWC01#
HQ-CMX-SWC01#
HQ-CMX-SWC01#show spanning-tree root

                                        Root    Hello Max Fwd
Vlan                   Root ID          Cost    Time  Age Dly  Root Port
---------------- -------------------- --------- ----- --- ---  ------------
VLAN0001             1 0cbd.8f1f.0000         0    2   20  15
VLAN0010            10 0cbd.8f1f.0000         0    2   20  15
VLAN0020            20 0c5f.9765.0000         6    2   20  15  Po3
VLAN0030            30 0c5f.9765.0000         6    2   20  15  Po3
VLAN0040            40 0cbd.8f1f.0000         0    2   20  15
HQ-CMX-SWC01#
```
<details open>
<summary><strong>Switch Core 02</strong></summary>
  
```text
HQ-CMX-SWC02#show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Gi0/0, Gi0/1, Gi0/2, Gi0/3
                                                Gi1/0, Gi1/3, Gi2/0, Gi2/3
                                                Gi3/0, Gi3/3
10   MANAGEMENT                       active
20   USERS                            active
30   VoIP                             active
40   SERVERS                          active
99   NATIVE                           active
999  BLACKHOLE                        active
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
HQ-CMX-SWC02#
HQ-CMX-SWC02#
HQ-CMX-SWC02#
HQ-CMX-SWC02#show etherchannel summary
Flags:  D - down        P - bundled in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      N - not in use, no aggregation
        f - failed to allocate aggregator

Number of channel-groups in use: 3
Number of aggregators:           3

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Gi1/1(P)    Gi1/2(P)
2      Po2(SU)         LACP      Gi2/1(P)    Gi2/2(P)
3      Po3(SU)         LACP      Gi3/1(P)    Gi3/2(P)

HQ-CMX-SWC02#
HQ-CMX-SWC02#
HQ-CMX-SWC02#
HQ-CMX-SWC02#show spanning-tree root

                                        Root    Hello Max Fwd
Vlan                   Root ID          Cost    Time  Age Dly  Root Port
---------------- -------------------- --------- ----- --- ---  ------------
VLAN0001          4097 0c5f.9765.0000         0    2   20  15
VLAN0010            10 0cbd.8f1f.0000         6    2   20  15  Po3
VLAN0020            20 0c5f.9765.0000         0    2   20  15
VLAN0030            30 0c5f.9765.0000         0    2   20  15
VLAN0040            40 0cbd.8f1f.0000         6    2   20  15  Po3
HQ-CMX-SWC02#
```
<details open>
<summary><strong>Switch Access 01</strong></summary>
  
```text
HQ-CMX-SWA01#show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Gi0/0, Gi0/1, Gi0/2, Gi0/3
                                                Gi1/0, Gi1/3, Gi2/0, Gi2/3
                                                Gi3/0, Gi3/1, Gi3/2, Gi3/3
10   MANAGEMENT                       active
20   USERS                            active
30   VoIP                             active
40   SERVERS                          active
99   NATIVE                           active
999  BLACKHOLE                        active
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
HQ-CMX-SWA01#
HQ-CMX-SWA01#
HQ-CMX-SWA01#
HQ-CMX-SWA01#show etherchannel summary
Flags:  D - down        P - bundled in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      N - not in use, no aggregation
        f - failed to allocate aggregator

Number of channel-groups in use: 2
Number of aggregators:           2

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Gi1/1(P)    Gi1/2(P)
2      Po2(SU)         LACP      Gi2/1(P)    Gi2/2(P)

HQ-CMX-SWA01#
HQ-CMX-SWA01#
HQ-CMX-SWA01#
HQ-CMX-SWA01#show spanning-tree root

                                        Root    Hello Max Fwd
Vlan                   Root ID          Cost    Time  Age Dly  Root Port
---------------- -------------------- --------- ----- --- ---  ------------
VLAN0001         36865 0ce9.7aec.0000         0    2   20  15
VLAN0010            10 0cbd.8f1f.0000         3    2   20  15  Po1
VLAN0020            20 0c5f.9765.0000         3    2   20  15  Po2
VLAN0030            30 0c5f.9765.0000         3    2   20  15  Po2
VLAN0040            40 0cbd.8f1f.0000         3    2   20  15  Po1
HQ-CMX-SWA01#
```

<details open>
<summary><strong>Switch Access 02</strong></summary>
  
```text
HQ-CMX-SWA02#show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Gi0/0, Gi0/1, Gi0/2, Gi0/3
                                                Gi1/0, Gi1/3, Gi2/0, Gi2/3
                                                Gi3/0, Gi3/1, Gi3/2, Gi3/3
10   MANAGEMENT                       active
20   USERS                            active
30   VoIP                             active
40   SERVERS                          active
99   NATIVE                           active
999  BLACKHOLE                        active
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
HQ-CMX-SWA02#
HQ-CMX-SWA02#
HQ-CMX-SWA02#
HQ-CMX-SWA02#show etherchannel summary
Flags:  D - down        P - bundled in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      N - not in use, no aggregation
        f - failed to allocate aggregator

Number of channel-groups in use: 2
Number of aggregators:           2

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Gi1/1(P)    Gi1/2(P)
2      Po2(SU)         LACP      Gi2/1(P)    Gi2/2(P)

HQ-CMX-SWA02#
HQ-CMX-SWA02#
HQ-CMX-SWA02#
HQ-CMX-SWA02#show spanning-tree root

                                        Root    Hello Max Fwd
Vlan                   Root ID          Cost    Time  Age Dly  Root Port
---------------- -------------------- --------- ----- --- ---  ------------
VLAN0001         36865 0c8a.68aa.0000         0    2   20  15
VLAN0010            10 0cbd.8f1f.0000         3    2   20  15  Po1
VLAN0020            20 0c5f.9765.0000         3    2   20  15  Po2
VLAN0030            30 0c5f.9765.0000         3    2   20  15  Po2
VLAN0040            40 0cbd.8f1f.0000         3    2   20  15  Po1
HQ-CMX-SWA02#
```

<details open>
<summary><strong>Switch Access 03</strong></summary>
  
```text
HQ-CMX-SWA03#show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Gi0/0, Gi0/1, Gi0/2, Gi0/3
                                                Gi1/0, Gi1/3, Gi2/0, Gi2/3
                                                Gi3/0, Gi3/1, Gi3/2, Gi3/3
10   MANAGEMENT                       active
20   USERS                            active
30   VoIP                             active
40   SERVERS                          active
99   NATIVE                           active
999  BLACKHOLE                        active
1002 fddi-default                     act/unsup
1003 token-ring-default               act/unsup
1004 fddinet-default                  act/unsup
1005 trnet-default                    act/unsup
HQ-CMX-SWA03#
HQ-CMX-SWA03#
HQ-CMX-SWA03#
HQ-CMX-SWA03#show etherchannel summary
Flags:  D - down        P - bundled in port-channel
        I - stand-alone s - suspended
        H - Hot-standby (LACP only)
        R - Layer3      S - Layer2
        U - in use      N - not in use, no aggregation
        f - failed to allocate aggregator

Number of channel-groups in use: 2
Number of aggregators:           2

Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Gi1/1(P)    Gi1/2(P)
2      Po2(SU)         LACP      Gi2/1(P)    Gi2/2(P)

HQ-CMX-SWA03#
HQ-CMX-SWA03#
HQ-CMX-SWA03#
HQ-CMX-SWA03#show spanning-tree root

                                        Root    Hello Max Fwd
Vlan                   Root ID          Cost    Time  Age Dly  Root Port
---------------- -------------------- --------- ----- --- ---  ------------
VLAN0001         36865 0c75.81fa.0000         0    2   20  15
VLAN0010            10 0cbd.8f1f.0000         3    2   20  15  Po1
VLAN0020            20 0c5f.9765.0000         3    2   20  15  Po2
VLAN0030            30 0c5f.9765.0000         3    2   20  15  Po2
VLAN0040            40 0cbd.8f1f.0000         3    2   20  15  Po1
HQ-CMX-SWA03#
```

