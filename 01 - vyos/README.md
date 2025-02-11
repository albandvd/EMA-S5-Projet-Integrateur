# VyOS : le routeur virtuel

## Installation de la VM:

### Config VmWare:

Ram: 1024Mb  
Proc: 1
Disque Dur: 4g

Retirer les périphériques "sound card", "printer" et "usb controller" qui ne sont pas utile pour ce projet. 

Attention, il faut verifier que le disque principale est un disque Sata car la commande d'installation de vyos ne marche pas avec les disques SCSI. Supprimez le disque dans "edit virtual machine settings" et rajoutez en un sata. 

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

```bash 
config
set system option keyboard-layout fr
commit 
save
```

## Homogénéisation des noms des interfaces

```bash 
config 
delete interfaces ethernet eth0 hw-id
commit
save
```