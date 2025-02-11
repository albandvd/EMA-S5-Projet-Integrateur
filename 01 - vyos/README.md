# VyOS : le routeur virtuel

## Installation de la VM:

### Config VmWare:

Ram: 1024Mb  
Proc: 1
Disque Dur: 4g (SATA)

Retirer les périphériques "sound card", "printer" et "usb controller" qui ne sont pas utile pour ce projet. 

Attention, il faut verifier que le disque principale est un disque Sata car la commande d'installation de vyos ne marche pas avec les disques SCSI (disque par defaut sur VMware). Supprimez le disque dans "edit virtual machine settings" et rajoutez en un sata. 

### Installation de l'OS

```bash 
sudo loadkeys fr #passer le clavier en fr pour faciliter l'installation

tce-load -wi tc-install #installation de l'installateur
sudo install image
# puis entrer cette suite d'argument: c, f, 1, 2, y, n, 3, vge=788 tce=hda1, y

reboot 
```

Ne pas oublier d'enlever l'iso avant de faire le reboot. 
Si l'installation s'est bien passé le clavier est de nouveau en qwerty et le /dev contient sda1, sda2 et sda3.
Si l'installation n'arrive pas a son terme cela signifie que l'installateur ne detecte pas le disque refaire la manipulation detaillé à la fin de la config VMware. 

## Clavier Azerty

Les machines vyos ont deux modes de configurations, le mode exploitation qui permet d'afficher l'état de la machine, les interfaces et les configurations actives mais aussi le mode de configuration qui permet de modifier de manière percistantes les configurations du routeur. On va donc utiliser ce mode la modifier la langue du clavier 

```bash 
config #entre en mode configuration 
set system option keyboard-layout fr #modification du clavier
commit #application des modifications instantanemant
save # sauvegarde de la configuration la percistance
```

## Homogénéisation des noms des interfaces

Les machines vyos et les machines basées sur Debian ont un kw-id (hardware id) qui correspond à une adresse mac associé à l'interface réseau cette dernière est générée par l'os en plus de l'adresse MAC physique. Lors du clonnage de la VM, l'os attribue une nouvelle adresse MAC à l'interface eth0 l'adresse étant différente que celle sur la machine hote, la machine va considérér que l'interface n'existe plus et va créer une nouvelle interface eth1 au lieu de eth0. 

Pour éviter ce problème il existe plusieurs solutions:

 - Solution 1: Suppressions des interfaces

Une solution possible est de créer une machine virtuelle sans interface ethernet parfaitement configuré et lors que l'on a besoin cloner la VM sans interface, puis rajouter des interfaces sur la machine. En faisant ca il n'y a pas d'interfaces clonées donc pas de hw-id. 

- Solution 2: Supressions du hw-id 

Une autre solution consiste à créer une machine virtuelle et de la configurer en enlevant le hw-id sur toutes les interfaces. De ce fait, lors ce que l'on clone, la machine génère un hw-id qui sera relié à l'interface vu que cette dernière n'en a pas initialement. Il va donc garder son nom initial eth0

```bash 
config 
delete interfaces ethernet eth0 hw-id
commit
save
```

Cette configuration est a réaliser sur toutes les interfaces de la machine que l'on veut clonner. 