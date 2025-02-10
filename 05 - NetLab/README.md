# NetLab: le réseau virtuel

Pour réaliser cette partie du projet nous allons configurer un "Lan Segment" pour chaque sous-réseau du NetLab et relier chaque interface de chaque machine à un Lan segment en fonction du tableau d'adressage fournit en annexe (Page 7-8).  
Il faudra remplacer les x dans le tableau par le numero 26 qui est mon numéro élève pour ce module. 

## Configuration des terminaux: Alpine Linux

### Configuration des interfaces

Dans VMware aller dans la configuration de la machine et passer l'interfaces de NAT à la Lan Segment: 

eth0 -> N2

### Mise en place des adresses IPv4
Ici on utilise le /etc/network/interfaces pour s'assurer de la pecistance de la configuration

``` bash 
vi /etc/network/interfaces

auto eth0
iface eth0 inet static
    address 10.26.3.104
    netmask 255.255.255.0
    gateway 10.26.3.1
```

## Configuration des terminaux: MicroCore

### Configuration des interfaces

Dans VMware aller dans la configuration de la machine et passer l'interfaces de NAT à la Lan Segment: 

eth0 -> N1

Ici on prend l'exemple du terminal T1 

### Mise en place des adresses IPv4 et IPv6

Ici on utilise le /etc/network/interfaces pour s'assurer de la pecistance de la configuration

``` bash 
sudo vi /etc/network/interfaces

ifconfig eth0 10.26.1.101 netmask 255.255.255.0 up
route add default gw 10.26.1.1

filetool.sh -b
```