# PROYECTO 2
### Integrantes:
| Nombre  | Carnet |
|---------------|---------|
| Eliezer Abraham Zapeta Alvarado   | 201801719  | 
| Christopher Iván Monterroso Alegria   | 201902363  | 

### Los pasos del proyecto serían:

1. **Realizar la topología**
2. **Conectar Routers y Switchs y conexion serial**
3. **Creacion de PortCHannel PAGP y LACP**
4. **Crear IP virtual HSRP para los routers establecidos**
5. **Configurar VPCs**
6. **Creación de rutas estáticas**

# CORE
| ROUTER     | RED      |
|------------|----------|
| JUTIAPA    | 0.0.0.63 |
| ESCUINTAL  | 0.0.0.63 |
| QUICHE     | 0.0.0.63 |
| PETÉN      | 0.0.0.63 |



# RESUMEN SEDES (ID)

| SEDE       | RED             |
|------------|-----------------|
| JUTIAPA    | 192.168.93.0/24 |
| ESCUINTAL  | 192.148.93.0/24 |
| QUICHE     | 192.178.93.0/24 |
| PETÉN      | 192.158.93.0/24 |


## JUTIAPA

1. **Primera IP = ID de red + 1**
2. **Broadcast = ID de red + Wildcard**
3. **Última IP = Broadcast - 1**
4. **Siguiente ID de red = Broadcast + 1**

| SEDE          | RED             |
|---------------|-----------------|
| JUTIAPA       | 192.168.93.0/24 |

| Departamento | VLAN ID | Equipos | Máscara de subred | Wildcard | ID de RED     | Primera IP    | Última IP     | Broadcast     |
|--------------|---------|---------|-------------------|----------|---------------|---------------|---------------|---------------| 
| RRHH         | 112     | 10      | 255.255.255.240   | 0.0.0.15 | 192.168.93.0  | 192.168.93.1  | 192.168.93.14 | 192.168.93.15 |
| CONTABILIDAD | 212     | 4       | 255.255.255.248   | 0.0.0.7  | 192.168.93.16 | 192.168.93.17 | 192.168.93.22 | 192.168.93.23 |
| VENTAS       | 312     | 25      | 255.255.255.224   | 0.0.0.31 | 192.168.93.24 | 192.168.93.25 | 192.168.93.54 | 192.168.93.55 |
| INFORMATICA  | 412     | 12      | 255.255.255.240   | 0.0.0.15 | 192.168.93.56 | 192.168.93.57 | 192.168.93.70 | 192.168.93.71 |

### Configuración LACP en SW2 Y SW3
### SW2
```
configure terminal
interface range f0/1-2
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
interface range f0/1-2
channel-group 1 mode passive
no shutdown
exit
interface port-channel 1
switchport mode trunk

exit
do write
```
### Verificando la configuración
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
interface Ethernet 0/1
ip address 192.X.X.X 255.X.X.X
no shutdown

!usamos la version 2 de HSRP
standby version 2

!definimos su id de grupo HSRP y la dirección ip virtual del gateway
standby 21 ip 192.X.X.X

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
interface Ethernet 0/1
ip address 192.X.X.X 255.X.X.X
no shutdown
standby version 2
standby 21 ip 192.X.X.X
do write
```
### Verificando la configuración
```
show standby
show standby brief
```

## ESCUINTLA

| SEDE          | RED             |
|---------------|-----------------|
| ESCUINTAL     | 192.148.93.0/24 |

| Departamento | VLAN ID | Equipos | Máscara de subred | Wildcard | ID de RED     | Primera IP   | Última IP     | Broadcast     |
|--------------|---------|---------|-------------------|----------|---------------|--------------|---------------|---------------|
| RRHH         | 112     | 5       | 255.255.255.248   | 0.0.0.7  | 192.148.93.0  | 192.148.93.1 | 192.148.93.6  | 192.148.93.7  |
| VENTAS       | 312     | 20      | 255.255.255.224   | 0.0.0.31 | 192.148.93.8  | 192.148.93.9 | 192.148.93.38 | 192.148.93.39 |

### Truncales para el Server
```
configure terminal
interface range Fa0/i-n
switchport trunk encapsulation dot1q
switchport mode trunk
```
### Truncales para los Clientes
```
configure terminal
interface Fa0/i
switchport trunk encapsulation dot1q
switchport mode trunk
```
### Configurar el modo cliente VTP en los switches clientes
```
configure terminal
vtp mode client
vtp domain dominio
vtp password contrasena
do write
```
### Configurar el modo servidor VTP en el switch servidor
```
configure terminal
vtp version 2
vtp mode server
vtp domain dominio
vtp password contrasena
do write
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
interface Fa0/i
switchport mode access
switchport access vlan <id>
interface Fa0/i
switchport mode access
switchport access vlan <id>
do write
```

### SERVIDOR Y CLIENTES STP
```
configure terminal
spanning-tree mode rapid-pvst
spanning-tree vlan 112,312 root primary
```
Con esto lograremos definir al switch como raíz y además indicarle las vlans con las que trabajará.



## QUICHE

| SEDE          | RED             |
|---------------|-----------------|
| QUICHE        | 192.178.93.0/24 |

| Departamento  | VLAN ID | Equipos  | Máscara de subred | Wildcard | ID de RED     | Primera IP    | Última IP      | Broadcast      |
|---------------|---------|----------|-------------------|----------|---------------|---------------|----------------|----------------|
| RRHH          | 112     | 12       | 255.255.255.240   | 0.0.0.15 | 192.178.93.0  | 192.178.93.1  | 192.178.93.14  | 192.178.93.15  |
| CONTABILIDAD  | 212     | 10       | 255.255.255.240   | 0.0.0.15 | 192.178.93.16 | 192.178.93.17 | 192.178.93.30  | 192.178.93.31  | 
| VENTAS        | 312     | 36       | 255.255.255.192   | 0.0.0.63 | 192.178.93.32 | 192.178.93.33 | 192.178.93.94  | 192.178.93.95  |
| INFORMATICA   | 412     | 21       | 255.255.255.224   | 0.0.0.31 | 192.178.93.96 | 192.178.93.67 | 192.178.93.126 | 192.178.93.127 |


## PETÉN

| SEDE          | RED             |
|---------------|-----------------|
| PETÉN         | 192.158.93.0/24 |

| Departamento  | VLAN ID | Equipos  | Máscara de subred | Wildcard | ID de RED     | Primera IP    | Última IP     | Broadcast     |
|---------------|---------|----------|-------------------|----------|---------------|---------------|---------------|---------------|
| RRHH          | 112     | 10       | 255.255.255.240   | 0.0.0.15 | 192.158.93.0  | 192.158.93.1  | 192.158.93.14 | 192.158.93.15 |
| VENTAS        | 312     | 30       | 255.255.255.224   | 0.0.0.31 | 192.158.93.16 | 192.158.93.17 | 192.158.93.46 | 192.158.93.47 |
| INFORMATICA   | 412     | 15       | 255.255.255.224   | 0.0.0.31 | 192.158.93.48 | 192.158.93.49 | 192.158.93.78 | 192.158.93.79 |
