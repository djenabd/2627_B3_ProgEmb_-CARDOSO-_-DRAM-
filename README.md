# Tp 1 

**Réflexion Notez le hostname et le nom d'utilisateur choisis. Pourquoi est-il nécessaire de définir ces informations avant le premier démarrage d'une Raspberry Pi utilisée sans écran ?**

## 💭 Réflexion Sur votre compte rendu :
**Expliquez pourquoi TX est relié à RX et RX à TX.** \
TX c'est la broche de transmission et RX de réception, les deux sont reliés pour communiquer.

**Expliquez le rôle de GND dans cette liaison.** \
C'est la masse. Elle permet aux deux appareils de partager la même référence électrique.

**Que signifie le réglage 115200 8N1 ?** \
C'est une vitesse de 115200 bits par seconde, des données codées sur 8 bits sans bit de parité et avec 1 bit d'arrêt. C'est un format convenus entre l'émetteur et le récepteur.

**Pourquoi ne faut-il pas connecter la broche 5 V de l'adaptateur aux GPIO de la Raspberry Pi ?** \
Car les broches GPIO de la Raspberry Pi fonctionnent en 3,3 V. 5V c'est trop élevé, cette tension peut l'endommager .

**Que se passe-t-il si le terminal série est configuré à une autre vitesse que la Raspberry Pi ?** \
Les données reçues seront incorrectes ou illisibles car les deux appareils ne communiquent pas au même rythme.

**Dessinez un schéma de câblage représentant le sheild utiliser.**\ 

## 💭 Réflexion Comparez la connexion UART et la connexion SSH : quels équipements et quelles configurations sont nécessaires dans chaque cas ? Donnez un avantage et une limite de chaque méthode.
La connexion UART nécessite un adaptateur USB relié directement à la Raspberry Pi. Il permet d'accéder à la machine même lorsqu'elle n'est pas connectée à un réseau.\
Limite: il faut être physiquement proche de la carte.

La connexion SSH fonctionne via le réseau (Wi-Fi). Il permet d'accéder facilement à la Raspberry Pi à distance et de manière sécurisée. \
Limite: il faut que la carte soit correctement connectée au réseau et que le service SSH soit activé.

## 💭 Réflexion
**Notez l'adresse IP obtenue.** \
**Avez vous accès à internet ?** Oui \
**Pourquoi la commande sudo fonctionne ici ?** La commande sudo fonctionne car l'utilisateur créé a les droits nécessaires pour exécuter certaines commandes en mode admin.

## 💭 Réflexion Répondez aux questions suivantes :
**Où se trouve la clé privée ? Où se trouve la clé publique ?** \
Les deux clés sont stockés dans le dossier .ssh du PC.

**Pourquoi la clé privée ne doit-elle pas être copiée dans ~/.ssh/authorized_keys ?** \
La clé privée doit rester uniquement sur le PC du propriétaire. Si quelqu'un d'autre y a accès, il pourra se connecter à la Raspberry Pi.

**Quel est le rôle de authorized_keys ?** \
Le fichier authorized_keys contient toutes les clés publiques autorisées à se connecter à la Raspberry Pi. Lors d'une connexion SSH, le système vérifie que la clé correspond à l'une de celles enregistrées dans ce fichier.

**Quelle différence faites-vous entre le mot de passe du compte Raspberry Pi et la phrase secrète de la clé privée ?** \
Le mot de passe sert à se connecter au compte utilisateur de la Raspberry Pi. La phrase secrète elle sert à protéger la clé privée stockée sur le PC. C'est une double protection car même si quelqu'un récupère la clé privée, il ne pourra pas l'utiliser sans cette phrase secrète.

**Pourquoi faut-il tester une nouvelle connexion avant de désactiver l'authentification par mot de passe ?** \ 
Il faut vérifier que la connexion par clé fonctionne correctement, sinon, si on désactive trop tôt le mot de passe et que la clé ne fonctionne pas on risque de ne plus avoir accès à la Rasberry Pi.

**Quels droits doivent avoir les dossiers et fichiers .ssh pour limiter les risques ?** \
Les fichiers contenant les clés ne doivent être accessibles que par leur propriétaire. Cela évite qu'un autre utilisateur puisse consulter ou modifier les informations utilisées pour l'authentification SSH.

# TP 2

## 💭 Réflexion Répondez aux questions suivantes :
**Pourquoi un moteur ne doit-il pas être branché directement sur une broche GPIO ?** \
Car une broche GPIO ne peut pas fournir assez de courant pour alimenter un moteur. Cela risque d'endommager la Raspberry Pi, il faut utiliser un driver adapté pour le contrôler

**Quelle différence y a-t-il entre une adresse I2C et une sélection de périphérique SPI ?** \
Une adresse I2C permet d'identifier un périphérique parmi plusieurs sur les deux fils du bus tandis qu'en SPI la sélection du périphérique est gérée directement par le bus

**Pourquoi une communication UART nécessite-t-elle d'accorder le débit entre les deux appareils ?** \
Parce que les deux appareils doivent échanger les données au même rythme sinon les octets reçus risquent d'être mal interprétés

**Pourquoi les programmes des TP doivent-ils toujours fermer ou nettoyer les interfaces matérielles ?** \
Pour libérer les ressources utilisées et éviter de laisser les GPIO dans un mauvais état. Le bloc finally permet de garantir le nettoyage même si le programme est interrompu

**Quel est le rôle d'un driver et que gagne-t-on à séparer main.py, config.py et le driver ?** \
Le driver masque les détails de la communication matérielle, le programme principal peut donc appeler des fonctions comme read_accel() ou rotate() sans avoir à gérer les registres, les octets, les timings et les broches. Séparer les fichiers permet de mieux organiser le code et de distinguer le programme principal, la configuration et la communication avec le matériel.

