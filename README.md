## Abrimos Packet Tracer y buscamos los siguientes equipos:
- Router 2901
- Switch 2960
- 4 PC

## Procedimiento con el Router
- Apagamos el router
- Agregamos el componente 4ESW para tener puertos ethernet disponibles
- Encendemos
- Realizamos las conexiones (cableado)

<img width="762" height="582" alt="Captura de Pantalla 2026-10-05 a la(s) 9 30 16 p  m" src="https://github.com/user-attachments/assets/f6e3b96d-60f2-4a5f-a8d1-d81e64c2e3a7" />


## Creación de VLANS en Switch
- No vamos al CLI del Switch e ingresamos los siguiente

enable
configure terminal

vlan 10
name ADMINISTRACION

vlan 20
name VENTAS

end
write

## Asignamos puertos a las VLANS
configure terminal

interface range fa0/1-2
switchport mode access
switchport access vlan 10

interface range fa0/3-4
switchport mode access
switchport access vlan 20

end
write

##configure terminal

interface fa0/24
switchport mode trunk

end
writeConfiguramos el puerto trunk hacia el router

## Configuramos el router
enable
configure terminal
interface g0/0
no shutdown
exit

## Creamos subinterfaces VLAN10
interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

## Creamos subinterfaces VLAN20
interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0

## Configuración de laptops
- Ingresamos a cada laptop en a sección de "IP CONFIGURATION" y registramos las IP, máscara y gateway.
- PC1
IP: 192.168.10.10
Mask: 255.255.255.0
Gateway: 192.168.10.1

- PC2
IP: 192.168.10.11
Mask: 255.255.255.0
Gateway: 192.168.10.1

- PC3
IP: 192.168.20.10
Mask: 255.255.255.0
Gateway: 192.168.20.1

- PC4
IP: 192.168.20.11
Mask: 255.255.255.0
Gateway: 192.168.20.1

## Verificamos con ping de pc a pc, se deben comunicar dentro de cada Vlan pero no de Vlan diferentes.

