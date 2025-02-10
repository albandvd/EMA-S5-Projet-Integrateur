# Verification de la configuration

## Verification de l'adressage

### Sur Vyos

```bash
show interfaces | match "inet"
show interfaces | match "inet6"

show ip route 
show ipv6 route 

show ip ospf neighbor
show ip route ospf

show ipv6 ospf neighbor
show ipv6 route ospf
```

### Sur Alpine et Microcore

``` bash 
ip addr show
ip -6 addr show scope link

ip route show default
ip -6 route show default

reboot 

# refaire la procédure pour vérifier la percistance
```

## Test de la connectivitée

``` Bash 
# Depuis R0 

ping 10.26.5.0
ping 2001:0:26:5::

ping 10.26.3.0
ping -6 2001:0:26:3::1

# si tous les pings sont réussi, cela atteste d'une connectivitée totale dans le réseau 

# Depuis T1 

ping 10.26.1.1

ping 10.26.2.102
ping 10.26.3.103
ping 10.26.3.104
ping 172.16.0.26
```

## Trouble-Shooting 

Force ca marche de mon côté