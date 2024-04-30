# PROYECTO 2
### Integrantes:
| Nombre  | Carnet |
|---------------|---------|
| Eliezer Abraham Zapeta Alvarado   | 201801719  | 
| Christopher Iván Monterroso Alegria   | 201902363  | 

### Calcular VLSM:
1. **Primera IP = ID de red + 1**
2. **Broadcast = ID de red + Wildcard**
3. **Última IP = Broadcast - 1**
4. **Siguiente ID de red = Broadcast + 1**

# RESUMEN SEDES (ID)
| SEDE       | RED             |
|------------|-----------------|
| JUTIAPA    | 192.168.93.0/24 |
| ESCUINTAL  | 192.148.93.0/24 |
| QUICHE     | 192.178.93.0/24 |
| PETÉN      | 192.158.93.0/24 |

## CORE
## FLSM - ROUTER CENTRAL
| ROUTER     | Equipos | Máscara de subred | ID de RED     | Primera IP    | Última IP     | Broadcast  |
|------------|---------|-------------------|---------------|---------------|---------------|------------|
| JUTIAPA    | 62      | 255.255.255.192   | 10.0.0.0      | 10.0.0.1      | 10.0.0.62	   | 10.0.0.63  |
| ESCUINTAL  | 62      | 255.255.255.192   | 10.0.0.64     | 10.0.0.65	   | 10.0.0.126	   | 10.0.0.127 |
| QUICHE     | 62      | 255.255.255.192   | 10.0.0.128    | 10.0.0.129    | 10.0.0.190    | 10.0.0.191 |
| PETÉN      | 62      | 255.255.255.192   | 10.0.0.192    | 10.0.0.193    | 10.0.0.254    | 10.0.0.255 |

## Configuracion OSPF
El protocolo OSPF es un protocolo de enrutamiento dinámico que se utiliza en los routers a los cuales queremos establecer las conexiones.

### Router central
```
configure terminal

interface FastEthernet0/0
ip address 10.0.0.1 255.255.255.252
no shutdown

interface FastEthernet1/0
ip address 10.0.0.5 255.255.255.252
no shutdown

interface FastEthernet2/0
ip address 10.0.0.9 255.255.255.252
no shutdown

interface FastEthernet3/0
ip address 10.0.0.13 255.255.255.252
no shutdown

router ospf 10
network 10.0.0.0 0.0.0.3 area 0
network 10.0.0.4 0.0.0.3 area 0
network 10.0.0.8 0.0.0.3 area 0
network 10.0.0.12 0.0.0.3 area 0

do write
```
### Router Quiche
```
configure terminal

interface FastEthernet2/0
ip address 10.0.0.2 255.255.255.252
no shutdown

interface FastEthernet3/0
ip address 10.0.0.6 255.255.255.252
no shutdown

interface FastEthernet4/0
ip address 10.0.0.10 255.255.255.252
no shutdown

interface FastEthernet5/0
ip address 10.0.0.14 255.255.255.252
no shutdown

router ospf 10
network 10.0.0.0 0.0.0.3 area 0
network 10.0.0.4 0.0.0.3 area 0
network 10.0.0.8 0.0.0.3 area 0
network 10.0.0.12 0.0.0.3 area 0

do write
```
### Router Jutiapa
```
configure terminal

interface FastEthernet2/0
ip address 10.0.0.3 255.255.255.252
no shutdown

interface FastEthernet3/0
ip address 10.0.0.7 255.255.255.252
no shutdown

interface FastEthernet4/0
ip address 10.0.0.11 255.255.255.252
no shutdown

interface FastEthernet5/0
ip address 10.0.0.15 255.255.255.252
no shutdown

router ospf 10
network 10.0.0.0 0.0.0.3 area 0
network 10.0.0.4 0.0.0.3 area 0
network 10.0.0.8 0.0.0.3 area 0
network 10.0.0.12 0.0.0.3 area 0

do write
```
### Router Escuintla
```
configure terminal

interface FastEthernet1/0
ip address 10.0.0.4 255.255.255.252
no shutdown

interface FastEthernet2/0
ip address 10.0.0.8 255.255.255.252
no shutdown

interface FastEthernet3/0
ip address 10.0.0.12 255.255.255.252
no shutdown

interface FastEthernet4/0
ip address 10.0.0.16 255.255.255.252
no shutdown

router ospf 10
network 10.0.0.0 0.0.0.3 area 0
network 10.0.0.4 0.0.0.3 area 0
network 10.0.0.8 0.0.0.3 area 0
network 10.0.0.12 0.0.0.3 area 0

do write
```
### Router Peten
```
configure terminal

interface FastEthernet1/0
ip address 10.0.0.5 255.255.255.252
no shutdown

interface FastEthernet2/0
ip address 10.0.0.9 255.255.255.252
no shutdown

interface FastEthernet3/0
ip address 10.0.0.13 255.255.255.252
no shutdown

interface FastEthernet4/0
ip address 10.0.0.17 255.255.255.252
no shutdown

router ospf 10
network 10.0.0.0 0.0.0.3 area 0
network 10.0.0.4 0.0.0.3 area 0
network 10.0.0.8 0.0.0.3 area 0
network 10.0.0.12 0.0.0.3 area 0

do write
```







## JUTIAPA

| SEDE          | RED             |
|---------------|-----------------|
| JUTIAPA       | 192.168.93.0/24 |

| Departamento | VLAN ID | Equipos | Máscara de subred | Wildcard | ID de RED     | Primera IP    | Última IP     | Broadcast     |
|--------------|---------|---------|-------------------|----------|---------------|---------------|---------------|---------------| 
| VENTAS       | 312     | 25      | 255.255.255.224   | 0.0.0.31 | 192.168.93.0  | 192.168.93.1  | 192.168.93.30 | 192.168.93.31 |
| INFORMATICA  | 412     | 12      | 255.255.255.240   | 0.0.0.15 | 192.168.93.32 | 192.168.93.33 | 192.168.93.46 | 192.168.93.47 |
| RRHH         | 112     | 10      | 255.255.255.240   | 0.0.0.15 | 192.168.93.48 | 192.168.93.49 | 192.168.93.62 | 192.168.93.63 |
| CONTABILIDAD | 212     | 4       | 255.255.255.248   | 0.0.0.7  | 192.168.93.64 | 192.168.93.65 | 192.168.93.70 | 192.168.93.71 |
### Configuracion de VPCS
| Departamento | Nombre | IP             | Máscara de subred | Puerta Enlace  | 
|--------------|--------|----------------|-------------------|----------------|
| RRHH         | VPC14  | 192.168.93.50  | 255.255.255.240   | 192.168.93.49  |
| RRHH         | VPC8   | 192.168.93.51  | 255.255.255.240   | 192.168.93.49  |
| CONTABILIDAD | VPC6   | 192.168.93.66  | 255.255.255.248   | 192.168.93.65  |
| CONTABILIDAD | VPC7   | 192.168.93.67  | 255.255.255.248   | 192.168.93.65  |
| VENTAS       | VPC5   | 192.168.93.2   | 255.255.255.224   | 192.168.93.1   |
| INFORMATICA  | VPC15  | 192.168.93.34  | 255.255.255.240   | 192.168.93.33  |
### ROUTER J1 Y J2
```
configure terminal

interface FastEthernet0/0.112   
encapsulation dot1Q 112
ip address 192.168.93.49 255.255.255.240 # RRHH

interface FastEthernet0/0.212
encapsulation dot1Q 212
ip address 192.168.93.65 255.255.255.248 # CONTABILIDAD

interface FastEthernet0/0.312
encapsulation dot1Q 312
ip address 192.168.93.1 255.255.255.224 # VENTAS

interface FastEthernet0/0.412
encapsulation dot1Q 412
ip address 192.168.93.33 255.255.255.240 # INFORMATICA
```
### Configuracion de VLANS SW2, SW3 y ESW1
```
configure terminal
vlan 112
name RRHH
vlan 212
name CONTABILIDAD
vlan 312
name VENTAS
vlan 412
name INFORMATICA
end
```
### Asignar el modo de acceso SW2.
```
configure terminal
interface Fa0/5
switchport mode access
switchport access vlan 112
interface Fa0/6
switchport mode access
switchport access vlan 112  # RRHH

interface Fa0/4
switchport mode access
switchport access vlan 212  # CONTABILIDAD
```
### Asignar el modo de acceso SW3.
```
configure terminal
interface Fa0/5
switchport mode access
switchport access vlan 212  # RRHH

interface Fa0/4
switchport mode access
switchport access vlan 312  # CONTABILIDAD

interface Fa0/6
switchport mode access
switchport access vlan 412  # CONTABILIDAD
```
### Troncales SW2, SW3 y ESW1
```
SW2
configure terminal
interface range Fa0/1
switchport mode trunk
exit

SW3
configure terminal
interface range Fa0/1
switchport mode trunk
exit

ESW1
configure terminal
interface range Fa0/1-4
switchport trunk encapsulation dot1q
switchport mode trunk
exit
```
### Configuración LACP en SW2 Y SW3
### SW2
```
configure terminal
interface range f0/2-3
channel-group 1 mode active
no shutdown
exit
interface port-channel 1
switchport mode trunk

exit
do write
```
### SW3
```
configure terminal
interface range f0/2-3
channel-group 1 mode passive
no shutdown
exit
interface port-channel 1
switchport mode trunk

exit
do write
```
### Verificando la configuración LACP
```
show etherchannel summary
enable
show running-config
show etherchannel
```
### Configuración HSRP Router J1 Y Router J2
### J1
```
enable
configure terminal
!le definimos su nombre
hostname J1

!configuramos la interfaz
interface FastEthernet 0/0
ip address 192.167.93.2 255.255.255.0
no shutdown

!usamos la version 2 de HSRP
standby version 2

!definimos su id de grupo HSRP y la dirección ip virtual del gateway
standby 21 ip 192.167.93.1

!también le definimos su prioridad
standby 21 priority 109

!configuramos el preempt, que sirve para que recupere la prioridad una se recupere la comunicación
standby 21 preempt

!guardamos
do write
```
### J2
```
enable
configure terminal
hostname J2
interface FastEthernet 0/0
ip address 192.167.93.3 255.255.255.0
no shutdown
standby version 2
standby 21 ip 192.167.93.1
do write
```
### Verificando la configuración
```
show standby
show standby brief
```
### Configurar el modo servidor VTP en el switch servidor ESW1
```
configure terminal
vtp version 2
vtp mode server
vtp domain 93
vtp password usac
do write
show vtp status
```
### Servidor STP ESW1, Protocolo RPVST
```
configure terminal
spanning-tree mode rapid-pvst
spanning-tree vlan 112,212,312,412 root primary
show spanning-tree
```
# Configuración de protocolo RIP
### Router Jutiapa
```
configure terminal

interface f0/0
ip address 12.0.0.2 255.255.255.0
no shutdown

interface f1/0
ip address 11.0.0.2 255.255.255.0
no shutdown

router rip
version 2

!definimos las redes conectadas a este router
network 12.0.0.0
network 11.0.0.0

do write

show ip protocol
show ip route
```
### Router J1
```
#J1
configure terminal

interface f1/0
ip address 12.0.0.1 255.255.255.0
no shutdown

router rip
version 2

!definimos las redes conectadas a este router
network 12.0.0.0
network 192.168.93.0

do write

show ip protocol
show ip route
```
### Router J2
```
#J2
configure terminal

interface f1/0
ip address 11.0.0.1 255.255.255.0
no shutdown

router rip
version 2

!definimos las redes conectadas a este router
network 11.0.0.0
network 192.168.93.0

do write

show ip protocol
show ip route
```











## QUICHE

| SEDE          | RED             |
|---------------|-----------------|
| QUICHE        | 192.178.93.0/24 |

| Departamento  | VLAN ID | Equipos  | Máscara de subred | Wildcard | ID de RED      | Primera IP     | Última IP      | Broadcast      |
|---------------|---------|----------|-------------------|----------|----------------|----------------|----------------|----------------|
| VENTAS        | 312     | 36       | 255.255.255.192   | 0.0.0.63 | 192.178.93.0   | 192.178.93.1   | 192.178.93.62  | 192.178.93.63  |
| INFORMATICA   | 412     | 21       | 255.255.255.224   | 0.0.0.31 | 192.178.93.64  | 192.178.93.65  | 192.178.93.94  | 192.178.93.95  |
| RRHH          | 112     | 12       | 255.255.255.240   | 0.0.0.15 | 192.178.93.96  | 192.178.93.97  | 192.178.93.110 | 192.178.93.111 |
| CONTABILIDAD  | 212     | 10       | 255.255.255.240   | 0.0.0.15 | 192.178.93.112 | 192.178.93.113 | 192.178.93.126 | 192.178.93.127 | 
### Configuracion de VPCS
| Departamento | Nombre | IP             | Máscara de subred | Puerta Enlace  | 
|--------------|--------|----------------|-------------------|----------------|
| RRHH         | PC22   | 192.178.93.98  | 255.255.255.240   | 192.178.93.97  |
| RRHH         | PC8    | 192.178.93.99  | 255.255.255.240   | 192.178.93.97  |
| CONTABILIDAD | PC19   | 192.178.93.114 | 255.255.255.240   | 192.178.93.113 | 
| CONTABILIDAD | PC9    | 192.178.93.115 | 255.255.255.240   | 192.178.93.113 |
| VENTAS       | PC20   | 192.178.93.2   | 255.255.255.192   | 192.178.93.1   |
| VENTAS       | PC11   | 192.178.93.3   | 255.255.255.192   | 192.178.93.1   |
| INFORMATICA  | PC21   | 192.178.93.66  | 255.255.255.224   | 192.178.93.65  |
### ROUTER QUICHE
```
configure terminal

interface FastEthernet0/0.112   
encapsulation dot1Q 112
ip address 192.178.93.97 255.255.255.240 # RRHH

interface FastEthernet0/0.212
encapsulation dot1Q 212
ip address 192.178.93.113 255.255.255.240 # CONTABILIDAD

interface FastEthernet0/0.312
encapsulation dot1Q 312
ip address 192.178.93.1 255.255.255.192 # VENTAS

interface FastEthernet0/0.412
encapsulation dot1Q 412
ip address 192.178.93.65 255.255.255.224 # INFORMATICA
```
### Troncales hacia el Router Escuintla
### SW1
```
configure terminal
interface range Fa0/1
switchport mode trunk
exit
```
### SW3
```
configure terminal
interface range Fa0/1
switchport mode trunk
exit
```
### Crear las VLAN en SW1 Y SW3
```
configure terminal
vlan 112
name RRHH
vlan 212
name CONTABILIDAD
vlan 312
name VENTAS
vlan 412
name INFORMATICA
end
```
### Asignar el modo de acceso SW1.
```
configure terminal
interface Fa0/2
switchport mode access
switchport access vlan 112  # RRHH

interface Fa0/3
switchport mode access
switchport access vlan 212  # CONTABILIDAD

interface Fa0/4
switchport mode access
switchport access vlan 312  # VENTAS

interface Fa0/5
switchport mode access
switchport access vlan 412  # INFORMATICA
do write
```
### Asignar el modo de acceso SW3.
```
configure terminal
interface Fa0/2
switchport mode access
switchport access vlan 112  # RRHH

interface Fa0/3
switchport mode access
switchport access vlan 212  # CONTABILIDAD

interface Fa0/4
switchport mode access
switchport access vlan 312  # VENTAS
do write
```











## ESCUINTLA

| SEDE          | RED             |
|---------------|-----------------|
| ESCUINTAL     | 192.148.93.0/24 |

| Departamento | VLAN ID | Equipos | Máscara de subred | Wildcard | ID de RED      | Primera IP    | Última IP      | Broadcast     |
|--------------|---------|---------|-------------------|----------|----------------|---------------|----------------|---------------|
| VENTAS       | 312     | 20      | 255.255.255.224   | 0.0.0.31 | 192.148.93.0   | 192.148.93.1  | 192.148.93.30  | 192.148.93.31 |
| RRHH         | 112     | 5       | 255.255.255.248   | 0.0.0.7  | 192.148.93.32  | 192.148.93.33 | 192.148.93.38  | 192.148.93.39 |
### Configuracion de VPCS
| Departamento | Nombre | IP             | Máscara de subred | Puerta Enlace  | 
|--------------|--------|----------------|-------------------|----------------|
| RRHH         | PC2    | 192.148.93.34  | 255.255.255.248   | 192.148.93.33  |
| VENTAS       | PC3    | 192.148.93.2   | 255.255.255.224   | 192.148.93.1   |
### ROUTER ESCUINTLA
```
configure terminal
interface FastEthernet0/0.112   
encapsulation dot1Q 112
ip address 192.148.93.33 255.255.255.248 # RRHH

interface FastEthernet0/0.312
encapsulation dot1Q 312
ip address 192.148.93.1 255.255.255.224 # VENTAS
```
### Configurar el modo servidor VTP en el switch servidor
```
configure terminal
vtp version 2
vtp mode server
vtp domain 93
vtp password usac
do write
```
### Troncal hacia el Router Escuintla
```
configure terminal
interface range Fa0/1
switchport mode trunk
exit
```
### Crear las VLAN en el switch que será el servidor
```
configure terminal
vlan 112
name RRHH
vlan 212
name CONTABILIDAD
vlan 312
name VENTAS
vlan 412
name INFORMATICA
end
```
### Asignar el modo de acceso con VLAN a los enlaces correspondientes.
```
configure terminal
interface Fa0/2
switchport mode access
switchport access vlan 112  # RRHH
interface Fa0/3
switchport mode access
switchport access vlan 312  # VENTAS
do write
```
Con esto lograremos definir al switch como raíz y además indicarle las vlans con las que trabajará.
### Servidor STP, Protocolo RPVST
```
configure terminal
spanning-tree mode rapid-pvst
spanning-tree vlan 112,212,312,412 root primary
show spanning-tree
```










## PETÉN

| SEDE          | RED             |
|---------------|-----------------|
| PETÉN         | 192.158.93.0/24 |

| Departamento  | VLAN ID | Equipos  | Máscara de subred | Wildcard | ID de RED     | Primera IP    | Última IP     | Broadcast     |
|---------------|---------|----------|-------------------|----------|---------------|---------------|---------------|---------------|
| VENTAS        | 312     | 30       | 255.255.255.224   | 0.0.0.31 | 192.158.93.0  | 192.158.93.1  | 192.158.93.30 | 192.158.93.31 |
| INFORMATICA   | 412     | 15       | 255.255.255.224   | 0.0.0.31 | 192.158.93.32 | 192.158.93.33 | 192.158.93.62 | 192.158.93.63 |
| RRHH          | 112     | 10       | 255.255.255.240   | 0.0.0.15 | 192.158.93.64 | 192.158.93.65 | 192.158.93.78 | 192.158.93.79 |

### Configuracion de VPCS
| Departamento | Nombre | IP             | Máscara de subred | Puerta Enlace  | 
|--------------|--------|----------------|-------------------|----------------|
| RRHH         | PC4    | 192.158.93.66  | 255.255.255.240   | 192.158.93.65  |
| VENTAS       | PC5    | 192.158.93.2   | 255.255.255.224   | 192.158.93.1   |
| INFORMATICA  | PC6    | 192.158.93.34  | 255.255.255.224   | 192.158.93.33  |

### ROUTER PETÉN
```
configure terminal
interface FastEthernet0/0.112   
encapsulation dot1Q 112
ip address 192.158.93.65 255.255.255.240 # RRHH

interface FastEthernet0/0.312
encapsulation dot1Q 312
ip address 192.158.93.1 255.255.255.224 # VENTAS

interface FastEthernet0/0.412
encapsulation dot1Q 412
ip address 192.158.93.33 255.255.255.224 # INFORMATICA
```
### Configurar el modo servidor VTP en el switch servidor
```
configure terminal
vtp version 2
vtp mode server
vtp domain 93
vtp password usac
do write
show vtp status
```
### Troncal hacia el Router PETÉN
```
configure terminal
interface range Fa0/1
switchport trunk encapsulation dot1q
switchport mode trunk
exit
```
### Crear las VLAN en el switch que será el servidor
```
configure terminal
vlan 112
name RRHH
vlan 212
name CONTABILIDAD
vlan 312
name VENTAS
vlan 412
name INFORMATICA
end
```
### Asignar el modo de acceso con VLAN a los enlaces correspondientes.
```
configure terminal
interface Fa0/2
switchport mode access
switchport access vlan 112  # RRHH
interface Fa0/3
switchport mode access
switchport access vlan 312  # VENTAS
interface Fa0/4
switchport mode access
switchport access vlan 412  # INFORMATICA
do write
```
Con esto lograremos definir al switch como raíz y además indicarle las vlans con las que trabajará.
### Servidor STP, Protocolo RPVST
```
configure terminal
spanning-tree mode rapid-pvst
spanning-tree vlan 112,212,312,412 root primary
show spanning-tree
```
