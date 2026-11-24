## HQ-CMX-RTR01 (Router Core 01)

|Source Device|Source Interface|Destination Device|Destination Interface|Description|
|-|-|-|-|-|
|HQ-CMX-RTR01|GigabitEthernet0/0|RTR-ISP01|GigabitEthernet0/0|Link to ISP Router|
|HQ-CMX-RTR01|GigabitEthernet1/0|HQ-CMX-SWC01|GigabitEthernet0/1|Link to Switch Core 01|
|HQ-CMX-RTR01|GigabitEthernet2/0|HQ-CMX-SWC02|GigabitEthernet0/1|Link to Switch Core 02|

##

## HQ-CMX-RTR02 (Router Core 02)

|Source Device|Source Interface|Destination Device|Destination Interface|Description|
|-|-|-|-|-|
|HQ-CMX-RTR02|GigabitEthernet0/0|RTR-ISP02|GigabitEthernet0/0|Link to ISP Router|
|HQ-CMX-RTR02|GigabitEthernet1/0|HQ-CMX-SWC01|GigabitEthernet0/2|Link to Switch Core 01|
|HQ-CMX-RTR02|GigabitEthernet2/0|HQ-CMX-SWC02|GigabitEthernet0/2|Link to Switch Core 02|

##

## HQ-CMX-SWC01 (Switch Core 01)

|Source Device|Source Interface|Destination Device|Destination Interface|Description|
|-|-|-|-|-|
|HQ-CMX-SWC01|GigabitEthernet0/1|HQ-CMX-RTR01|GigabitEthernet1/0|Link to Router Core 01|
|HQ-CMX-SWC01|GigabitEthernet0/2|HQ-CMX-RTR02|GigabitEthernet1/0|Link to Router Core 02|
|HQ-CMX-SWC01|GigabitEthernet1/1|HQ-CMX-SWA01|GigabitEthernet1/1|Link to Switch Access 01 (Po1)|
|HQ-CMX-SWC01|GigabitEthernet1/2|HQ-CMX-SWA01|GigabitEthernet1/2|Link to Switch Access 01 (Po1)|
|HQ-CMX-SWC01|GigabitEthernet2/1|HQ-CMX-SWA02|GigabitEthernet1/1|Link to Switch Access 02 (Po2)|
|HQ-CMX-SWC01|GigabitEthernet2/2|HQ-CMX-SWA02|GigabitEthernet1/2|Link to Switch Access 02 (Po2)|
|HQ-CMX-SWC01|GigabitEthernet3/1|HQ-CMX-SWA03|GigabitEthernet1/1|Link to Switch Access 03 (Po3)|
|HQ-CMX-SWC01|GigabitEthernet3/2|HQ-CMX-SWA03|GigabitEthernet1/2|Link to Switch Access 03 (Po3)|

## 

## HQ-CMX-SWC02 (Switch Core 02)

|Source Device|Source Interface|Destination Device|Destination Interface|Description|
|-|-|-|-|-|
|HQ-CMX-SWC02|GigabitEthernet0/1|HQ-CMX-RTR01|GigabitEthernet2/0|Link to Router Core 01|
|HQ-CMX-SWC02|GigabitEthernet0/2|HQ-CMX-RTR02|GigabitEthernet2/0|Link to Router Core 02|
|HQ-CMX-SWC02|GigabitEthernet1/1|HQ-CMX-SWA01|GigabitEthernet2/1|Link to Switch Access 01 (Po4)|
|HQ-CMX-SWC02|GigabitEthernet1/2|HQ-CMX-SWA01|GigabitEthernet2/2|Link to Switch Access 01 (Po4)|
|HQ-CMX-SWC02|GigabitEthernet2/1|HQ-CMX-SWA02|GigabitEthernet2/1|Link to Switch Access 02 (Po5)|
|HQ-CMX-SWC02|GigabitEthernet2/2|HQ-CMX-SWA02|GigabitEthernet2/2|Link to Switch Access 02 (Po5)|
|HQ-CMX-SWC02|GigabitEthernet3/1|HQ-CMX-SWA03|GigabitEthernet2/1|Link to Switch Access 03 (Po6)|
|HQ-CMX-SWC02|GigabitEthernet3/2|HQ-CMX-SWA03|GigabitEthernet2/2|Link to Switch Access 03 (Po6)|

## 

## HQ-CMX-SWA01 (Switch Access 01)

|Source Device|Source Interface|Destination Device|Destination Interface|Description|
|-|-|-|-|-|
|HQ-CMX-SWA01|GigabitEthernet1/1|HQ-CMX-SWC01|GigabitEthernet1/1|Link to Switch Core 01 (Po1)|
|HQ-CMX-SWA01|GigabitEthernet1/2|HQ-CMX-SWC01|GigabitEthernet1/2|Link to Switch Core 01 (Po1)|
|HQ-CMX-SWA01|GigabitEthernet2/1|HQ-CMX-SWC02|GigabitEthernet1/1|Link to Switch Core 02 (Po4)|
|HQ-CMX-SWA01|GigabitEthernet2/2|HQ-CMX-SWC02|GigabitEthernet1/2|Link to Switch Core 02 (Po4)|
|HQ-CMX-SWA01|GigabitEthernet0/0|HQ-CMX-PCV10|GigabitEthernet0|Link to PC in VLAN 10|
|HQ-CMX-SWA01|GigabitEthernet0/1|HQ-CMX-PCV20|GigabitEthernet0|Link to PC in VLAN 20|
|HQ-CMX-SWA01|GigabitEthernet0/2|HQ-CMX-PCV30|GigabitEthernet0|Link to PC in VLAN 30|
|HQ-CMX-SWA01|GigabitEthernet0/3|HQ-CMX-PCV40|GigabitEthernet0|Link to PC in VLAN 40|

## 

## HQ-CMX-SWA02 (Switch Access 02)

|Source Device|Source Interface|Destination Device|Destination Interface|Description|
|-|-|-|-|-|
|HQ-CMX-SWA02|GigabitEthernet1/1|HQ-CMX-SWC01|GigabitEthernet2/1|Link to Switch Core 01 (Po2)|
|HQ-CMX-SWA02|GigabitEthernet1/2|HQ-CMX-SWC01|GigabitEthernet2/2|Link to Switch Core 01 (Po2)|
|HQ-CMX-SWA02|GigabitEthernet2/1|HQ-CMX-SWC02|GigabitEthernet2/1|Link to Switch Core 02 (Po5)|
|HQ-CMX-SWA02|GigabitEthernet2/2|HQ-CMX-SWC02|GigabitEthernet2/2|Link to Switch Core 02 (Po5)|
|HQ-CMX-SWA02|GigabitEthernet0/0|HQ-CMX-PCV10|GigabitEthernet0|Link to PC in VLAN 10|
|HQ-CMX-SWA02|GigabitEthernet0/1|HQ-CMX-PCV20|GigabitEthernet0|Link to PC in VLAN 20|
|HQ-CMX-SWA02|GigabitEthernet0/2|HQ-CMX-PCV30|GigabitEthernet0|Link to PC in VLAN 30|
|HQ-CMX-SWA02|GigabitEthernet0/3|HQ-CMX-PCV40|GigabitEthernet0|Link to PC in VLAN 40|

## 

## HQ-CMX-SWA03 (Switch Access 03)

|Source Device|Source Interface|Destination Device|Destination Interface|Description|
|-|-|-|-|-|
|HQ-CMX-SWA03|GigabitEthernet1/1|HQ-CMX-SWC01|GigabitEthernet3/1|Link to Switch Core 01 (Po3)|
|HQ-CMX-SWA03|GigabitEthernet1/2|HQ-CMX-SWC01|GigabitEthernet3/2|Link to Switch Core 01 (Po3)|
|HQ-CMX-SWA03|GigabitEthernet2/1|HQ-CMX-SWC02|GigabitEthernet3/1|Link to Switch Core 02 (Po6)|
|HQ-CMX-SWA03|GigabitEthernet2/2|HQ-CMX-SWC02|GigabitEthernet3/2|Link to Switch Core 02 (Po6)|
|HQ-CMX-SWA03|GigabitEthernet0/0|HQ-CMX-PCV10|GigabitEthernet0|Link to PC in VLAN 10|
|HQ-CMX-SWA03|GigabitEthernet0/1|HQ-CMX-PCV20|GigabitEthernet0|Link to PC in VLAN 20|
|HQ-CMX-SWA03|GigabitEthernet0/2|HQ-CMX-PCV30|GigabitEthernet0|Link to PC in VLAN 30|
|HQ-CMX-SWA03|GigabitEthernet0/3|HQ-CMX-PCV40|GigabitEthernet0|Link to PC in VLAN 40|



