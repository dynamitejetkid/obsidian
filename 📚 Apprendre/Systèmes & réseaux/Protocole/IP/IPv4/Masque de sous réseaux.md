[Cours - Adresses IPv4 et calcul de masques](https://www.it-connect.fr/adresses-ipv4-et-le-calcul-des-masques-de-sous-reseaux/)

http://www.iplogos.fr/vlsm-les-masques-de-sous-reseaux-a-taille-variable/


[Calculateur de masques IPv4](https://cric.grenoble.cnrs.fr/Administrateurs/Outils/CalculMasque/)
[IP Calculator](http://jodies.de/ipcalc)
[Calculateur IP sous-réseau, CIDR](https://ceipam.eu/fr/ipcalculator.php)

Les bits à 1 dans le masque représentent la partie réseau. 
Les bits à 0 représentent la partie machine.


Première adresse du réseau : tous les bits de la partie machine sont à 0 - adresse du réseau, ne peut pas être utilisé pour une machine.
Dernière adresse du réseau : tous les bits de la partie machine sont à 1 - adresse de broadcast, permet d'identifier toutes les machines de mon réseau. Quand un message est envoyé à cette adresse, il est envoyé à toutes les machines de ce réseau. 

Nombre d’adresses dans un réseau : 2 puissance nombrede0danslemasque

#### Exemple entre 2 octets
Adresse [[IP]]
192.168.0.1 > **11000000.10101000**.00000000.00000001
Masque de sous réseau
255.255.0.0 > **11111111.11111111**.0000000.0000000

#### Exemple au milieu d'1 octet
Adresse [[IP]]
192.168.0.1 > **11000000.10101000.0000**0000.00000001
Masque de sous réseaux
255.255.240.0 > **1111111.11111111.1111**0000.00000000
On ne peut pas repasser en décimal lorsque la coupure a lieu au milieu d'un octet. On ne peut pas écrire une partie d'un octet, on peut donc uniquement s'exprimer en binaire. 

On retrouve toujours les mêmes valeurs pour les octets d'un masque : 
00000000 -> 0
10000000 -> 128
11000000 -> 192
11100000 -> 224
11110000 -> 240
11111000 -> 248
11111100 -> 252
11111110 -> 254
11111111 -> 255