# VPC ADMINISTRACION
ip 172.103.2.50 255.255.255.240 gateway 172.103.2.49
save

# VPC ACADEMICO
ip 172.103.2.2 255.255.255.224 gateway 172.103.2.1
save

# VPC INVESTIGACION
ip 172.103.2.34 255.255.255.240 gateway 172.103.2.33
save

# VPC SEGURIDAD
ip 172.103.2.66 255.255.255.248 gateway 172.103.2.65
save

# SWC
en
config t
hostname SWC
interface range e0/0-3
switchport trunk encapsulation dot1q
switchport mode trunk
duplex full
exit
interface range e0/0-1
channel-group 1 mode desirable
no shutdown
exit
interface range e0/2-3
channel-group 2 mode desirable
no shutdown
exit
interface e1/0
switchport trunk encapsulation dot1q
switchport mode trunk
duplex full
exit
vlan 13
name ACADEMICO
vlan 23
name INVESTIGACION
vlan 33
name ADMINISTRACION
vlan 43
name SEGURIDAD
exit
vtp version 2
vtp mode server
vtp domain proy2
vtp password proy2
spanning-tree mode rapid-pvst
spanning-tree vlan 13,23,33,43 root primary
no ip routing
exit
copy running-config startup-config

# SW1
en
config t
hostname SW1
vtp version 2
vtp mode client
vtp domain proy2
vtp password proy2
interface range e0/0-3
switchport trunk encapsulation dot1q
switchport mode trunk
duplex full
exit
interface range e0/0-1
channel-group 1 mode auto
no shutdown
exit
interface range e0/2-3
channel-group 3 mode auto
no shutdown
exit
interface e1/0
switchport mode access
switchport access vlan 33
exit
interface e1/1
switchport mode access
switchport access vlan 13
exit
spanning-tree mode rapid-pvst
no ip routing
exit
copy running-config startup-config

# SW2
en
config t
hostname SW2
vtp version 2
vtp mode client
vtp domain proy2
vtp password proy2
interface range e0/0-3
switchport trunk encapsulation dot1q
switchport mode trunk
duplex full
exit
interface range e0/0-1
channel-group 2 mode auto
no shutdown
exit
interface range e0/2-3
channel-group 3 mode desirable
no shutdown
exit
interface e1/0
switchport mode access
switchport access vlan 23
exit
interface e1/1
switchport mode access
switchport access vlan 43
exit
spanning-tree mode rapid-pvst
no ip routing
exit
copy running-config startup-config

# SW3
en
config t
hostname SW3
interface range e0/0-2
switchport trunk encapsulation dot1q
switchport mode trunk
duplex full
exit
no ip routing
exit
copy running-config startup-config

# R
en
config t
hostname R
interface e0/0
no shutdown
interface e0/0.13
encapsulation dot1q 13
ip address 172.103.2.1 255.255.255.224
interface e0/0.23
encapsulation dot1q 23
ip address 172.103.2.33 255.255.255.240
interface e0/0.33
encapsulation dot1q 33
ip address 172.103.2.49 255.255.255.240
interface e0/0.43
encapsulation dot1q 43
ip address 172.103.2.65 255.255.255.248
interface e0/1
ip address 172.103.0.4 255.255.255.248	
no shutdown
exit
ip route 172.103.0.0 255.255.255.248 172.103.0.1
ip route 9.0.0.0 255.255.255.240 172.103.0.1
ip route 10.0.0.0 255.255.255.240 172.103.0.1
ip route 11.0.0.0 255.255.255.240 172.103.0.1
ip route 173.103.0.0 255.255.255.248 172.103.0.1
ip route 173.103.2.0 255.255.255.0 172.103.0.1
exit
copy running-config startup-config

# C-1
en
config t
hostname C1
interface e0/0
ip address 172.103.0.2 255.255.255.248
no shutdown
standby version 2
standby 12 ip 172.103.0.1
standby 12 priority 110
standby 12 preempt
interface s1/0
ip address 9.0.0.1 255.255.255.252
no shutdown
exit
ip route 172.103.2.0 255.255.255.0 172.103.0.4
ip route 10.0.0.0 255.255.255.240 9.0.0.2
ip route 11.0.0.0 255.255.255.240 9.0.0.2
ip route 173.103.0.0 255.255.255.248 9.0.0.2
ip route 173.103.2.0 255.255.255.0 9.0.0.2
exit
copy running-config startup-config

# C-2
en
config t
hostname C2
interface e0/0
ip address 172.103.0.3 255.255.255.248
no shutdown
standby version 2
standby 12 ip 172.103.0.1
interface s1/0
ip address 9.0.0.5 255.255.255.252
no shutdown
exit
ip route 172.103.2.0 255.255.255.0 172.103.0.4
ip route 10.0.0.0 255.255.255.240 9.0.0.6
ip route 11.0.0.0 255.255.255.240 9.0.0.6
ip route 173.103.0.0 255.255.255.248 9.0.0.6
ip route 173.103.2.0 255.255.255.0 9.0.0.6
exit
copy running-config startup-config

# Central
en
config t
hostname Central
interface s1/0
ip address 9.0.0.2 255.255.255.252
no shutdown
interface s1/1
ip address 9.0.0.6 255.255.255.252
no shutdown
interface s1/2
ip address 10.0.0.5 255.255.255.252
no shutdown
interface s1/3
ip address 10.0.0.1 255.255.255.252
no shutdown
exit
ip route 172.103.2.0 255.255.255.0 9.0.0.1
ip route 172.103.2.0 255.255.255.0 9.0.0.5
ip route 172.103.0.0 255.255.255.248 9.0.0.1
ip route 172.103.0.0 255.255.255.248 9.0.0.5
ip route 11.0.0.0 255.255.255.240 10.0.0.6
ip route 11.0.0.0 255.255.255.240 10.0.0.2
ip route 173.103.0.0 255.255.255.248 10.0.0.6
ip route 173.103.0.0 255.255.255.248 10.0.0.2
ip route 173.103.2.0 255.255.255.0 10.0.0.6
ip route 173.103.2.0 255.255.255.0 10.0.0.2
exit
copy running-config startup-config
