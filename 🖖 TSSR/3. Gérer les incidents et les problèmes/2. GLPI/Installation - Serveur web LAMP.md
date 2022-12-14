[Installer GLPI 10 sur Debian](https://zatoufly.fr/installer-glpi-10-sur-debian/)

## Prérequis
### Installer Debian 11

### Définir une adresse IP statique

``` shell
#Afficher ma configuration IP
ip a
#Modifier en static
nano /etc/network/interfaces
#pour NAT sous VirtualBox, la gateway par défaut est 10.0.2.2
allow-hotplug enp0s3
iface enp0s3 inet static
  address 10.0.2.16/24
  gateway 10.0.2.2
#pour Bridge sous VirtualBox, la gateway est celle de ma machine
allow-hotplug enp0s3
iface enp0s3 inet static
  address 192.168.1.114/24
  gateway 192.168.1.1
```

Me connecter en SSH à mon serveur debian
```shell
ssh ben@192.168.1.114
```

Mettre à jour mon système :
``` shell
apt update && apt full-upgrade -y
```

## Installation du serveur LAMP

``` shell
#Installation Apache2 + MariaDB + PHP
apt install apache2 mariadb-server php -y
#Activer Apache2 + MariaDB au démarrage de la machine
systemctl enable apache2 mariadb
```

## Installation GLPI 10
 ```shell
#Installer Perl + extensions PHP
apt install perl -y
apt install php-ldap php-imap php-apcu php-xmlrpc php-cas php-mysqli php-mbstring php-curl php-gd php-simplexml php-xml php-intl php-zip php-bz2 -y

#Redémarrer Apache2
systemctl reload apache2
```

Téléchargement de la dernière version [ici](https://glpi-project.org/downloads/)
``` shell
#Téléchargement GLPI sur le site
cd /tmp/
wget https://github.com/glpi-project/glpi/releases/download/10.0.3/glpi-10.0.3.tgz

#Décompresser le fichier et le mettre dans /var/www/html/glpi
tar xzf glpi-10.0.3.tgz -C /var/www/html

	#Dézipper le fichier .tar.bz2
	tar -xvjf glpi-mydashboard-2.0.7.tar.bz2

	#Dézipper le fichier en .tar.gz
	tar -xzvf glpi-fusioninventory.tar.gz

	#Dézipper le fichier en .tar.xz
	tar -xJvf glpi-dashboard.tar.xz

#Changer les permissions sur le dossier GLPI pour que le serveur Apache puisse y accéder
chown -R www-data:www-data /var/www/html/glpi
chmod -R 775 /var/www/html/glpi
```

## Création de la base de données
J'utilise MariaDB pour la partie base de données (SQL)
Je vais créer la base de données, un utilisateur et la permission à ce dernier de travailler sur ma base de données.

``` shell
#Connexion au terminal MariaDB
mysql -u root

#Puis, dans le terminal de MariaDB :
create database glpi;
create user ben@localhost identified by "ben";
grant all privileges on glpi.* to ben@localhost;
flush privileges;
exit;
```

## Initialisation de GLPI 10

Sur mon navigateur, me connecter à http://IpServeur/glpi

![[Pasted image 20221016153939.png]]



``` shell
# Supprimer le fichier install/install.php
rm -f /var/www/html/glpi/install/install.php

# Activer les fuseaux horaires
mysql -u root  
	#dans MariaDB 
	GRANT SELECT ON `mysql`.`time_zone_name` TO 'ben'@'localhost';  
	FLUSH PRIVILEGES;  
	exit;

```

## En +
[Profils et créations d"utilisateurs sous GLPI](https://www.youtube.com/watch?v=eHxPKm0u04g)
[Création d'intitulés et de profils sous GLPI](https://www.youtube.com/watch?v=zsgo-Yg8gYo)
[Création de tickets sous GLPI](https://www.youtube.com/watch?v=y7hCPVjKVDI)
[Gestion des cartouches d'impression sous GLPI](https://www.youtube.com/watch?v=hZdtdX91Ovg)
[Base de connaissances GLPI](https://www.youtube.com/watch?v=88mOKwYL8PE&feature=youtu.be)
[Configurer les SLAs](https://www.youtube.com/watch?v=e8ANiaLQd2c)
[Intégration des utilisateurs AD à GLPI](https://www.youtube.com/watch?v=VLuY_tCsoyc)

