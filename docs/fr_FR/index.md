Configuration 
=============

Le plugin sms_custom permet de dialoguer avec Jeedom par l’intermediaire des
sms_custom, il permet aussi à Jeedom de vous envoyer un sms_custom en cas d’alerte
(plugin alarme, scénario…​)

> **Important**
>
> Pour dialoguer avec Jeedom il faut avoir configuré des interactions.

Configuration du plugin 
-----------------------

Après téléchargement du plugin, il vous suffit de l’activer et de
configurer le port. Après sauvegarde le démon devrait se lancer. Le
plugin est déjà configuré par défaut ; vous n’avez donc rien à faire de
plus. Cependant vous pouvez modifier cette configuration. Voici le
détail (certains paramètres peuvent n’être visibles qu’en mode expert) :

-   *Port sms_custom* : le port USB sur lequel votre clef GSM
        est connectée.

> **Tip**
>
> Si vous ne savez pas quel port USB est utilisé, vous pouvez simplement
> indiquer "Auto". Attention le mode auto ne marche qu’avec les clefs
> Huawai E220.

> **Important**
>
> Attention certaines clefs 3G sont par défaut en mode modem et non GSM.
> Il faut à l’aide du logiciel de votre fabricant de clef, changer le
> mode de la clef sur GSM (ou texte, ou série). 

-   **Code pin** : Permet d’indiquer le code pin de la carte SIM, à laisser vide si vous n’en avez pas. 
-   **Texte mode** : Mode de compatibilité étendu, à n’utiliser que si l’envoi et/ou la réception des messages ne marchent pas.
-   **Découper les messages par paquet de caractères** : Indique le nombre de caractères maximum par texto.
-   **Passerelle sms_custom / sms_custom Gateway (modifier en cas d’erreur : CMS 330 sms_customC number not set)** : A nechanger que si vous avez l’erreur "CMS 330 sms_customC number not set", dans ce cas il faut indiquer le numéro de passerelle sms_custom de votre opérateur téléphonique. 
-   **Force du signal** : Force de réception du signal devotre clef GSM.
-   **Réseau** : Réseau téléphonique de votre clef GSM (peut être à "None" si Jeedom n’arrive pas à le récupérer). 
-   **socket interne (modification dangereuse)** : permet de modifier le port de communication interne du démon.
-   **Cycle (s)** : cycle de scrutation du démon pour l'envoi et la reception des sms_custom. Un chiffre trop bas peut amener certaine instabilité

Configuration des équipements 
-----------------------------

La configuration des équipements sms_custom est accessible à partir du menu
plugin puis communication

Vous retrouvez ici toute la configuration de votre équipement :

-   **Nom de l’équipement sms_custom** : nom de votre équipement sms_custom,

-   **Activer** : permet de rendre votre équipement actif,

-   **Visible** : rend votre équipement visible sur le dashboard,

-   **Objet parent** : indique l’objet parent auquel
    appartient l’équipement.

En dessous vous retrouvez la liste des commandes :

-   **Nom** : le nom affiché sur le dashboard,

-   **Utilisateur** : utilisateur correspondant dans Jeedom (permet de
    restreindre certaines interactions à certains utilisateurs),

-   **Numéro** : numéro de téléphone à qui envoyer les messages. Vous
    pouvez mettre plusieurs numéros en les séparant avec des ; (ex
    : 0612345678;0698765432).

    > **Important**
    >
    > Seul les numéros de téléphone déclarés dans un équipement pouront
    > utiliser les interactions car seuls eux seront autorisés.

-   **Afficher** : permet d’afficher la donnée sur le dashboard,

-   **Configuration avancée** (petites roues crantées) : permet
    d’afficher la configuration avancée de la commande (méthode
    d’historisation, widget…​),

-   **Tester** : permet de tester la commande,

-   **Supprimer** (signe -) : permet de supprimer la commande.

Utilisation du plugin 
---------------------

Celui-ci est assez standard dans son fonctionnement, sur la page Général
→ Plugin puis en sélectionnant le plugin sms_custom :

-   Le port (chemin) jusqu’au périphérique qui sert de modem (par
    exemple ce peut être /dev/ttyUSB0, pour le voir il suffit de lancer
    “dmesg” puis de brancher le modem)

-   Le code pin de la carte sim

    Il faut donc ajouter un nouvel équipement puis le configurer :

-   Le nom de celui-ci,

-   S’il est actif ou non,

    Puis il faut ajouter les commandes qui seront composées d’un nom et
    d’un numéro, seuls les numéros listés dans la liste des commandes
    peuvent recevoir une réponse de Jeedom (cela permet de sécuriser,
    tout en évitant de mettre un mot de passe à chaque début de sms_custom
    envoyé à Jeedom). Vous pouvez aussi indiquer quel utilisateur est
    lié à ce numéro (pour la gestion des droits au niveau
    des interactions).

Pour communiquer avec Jeedom, il suffira ensuite de lui envoyer un
message à partir d’un numéro autorisé, toutes les interactions venant du
système d’interactions.

Petit exemple d’interaction : Question : “Quelle est la température de
la chambre ?” Réponse : “16.3 C”

Liste des clefs compatibles 
---------------------------

-   HUAWEI E220

-   Alcatel one touch X220L

-   HSDPA 7.2MBPS 3G Wireless

FAQ 
===

> **Je ne reçois rien avec une clef huwaei e160.**
>
>Il faut installer minicom (sudo apt-get install -y minicom), lancer
>celui-ci et se connecter au modem, puis faire :
>
>``` {.bash}
>AT^CURC=0
>AT^U2DIAG=0
>```
>
>Et sur le plugin faire :
>
>-   Choisir premier port USB et non le second
>
>-   Vitesse : 9600
>
>-   Mode texte désactivé

> **Je ne vois pas le port USB de ma clef**
>
>Vérifiez que vous n’avez pas brltty d’installer (`sudo apt-get remove brltty` pour le supprimer)

> **Au bout de quelques heures/jours je ne recois plus de sms_custom et ne peux plus en envoyer, une relance du démon corrige**
>
>Vérifiez votre cable USB (un mauvais cable USB entraine souvent ce
>genre de soucis, il ne faut pas qu’il soit trop long non plus),
>verifiez aussi votre alimentation, un hub USB est fortement
>conseillé

> **J’ai une erreur CME XX**
>
>Vous pouvez trouver [ici](:http://www.micromedia-int.com/fr/gsm-2/669-cme-error-gsm-equipment-related-errors) la description des differente erreurs CME

> **Configuration de la clef Alcatel one touch X220L**
>
>Lorsque l’on insère la clef, on a ceci :
>
>``` {.bash}
>root@jeedom:# lsusb
>Bus 002 Device 003: ID 1bbb:f000 T & A Mobile Phones
>```
>
>Attention si vous n’avez pas 1bbb:f000 il ne faut surtout pas faire la
>suite de cette documentation
>
>il faut ajouter les lignes suivantes à la fin du fichier
>/etc/usb\_modeswitch.conf :
>
>``` {.bash}
>########################################################
># Alcatel X220L
>DefaultVendor= 0x1bbb
>DefaultProduct= 0xf000
>MessageContent="55534243123456788000000080000606f50402527000000000000000000000"
>########################################################
>```
>
>Puis lancer la commande suivante pour tester :
>
>``` {.bash}
>/usr/sbin/usb_modeswitch -c
>/etc/usb_modeswitch.conf
>```
>
>On obtient ceci :
>
>``` {.bash}
>root@jeedom:~# lsusb
>Bus 002 Device 003: ID 1bbb:0017 T & A Mobile Phones
>```
>
>et les liens sous /dev sont bien ajoutés :
>
>``` {.bash}
>root@jeedom:~# ls /dev/ttyUSB*
>/dev/ttyUSB0 /dev/ttyUSB1 /dev/ttyUSB2 /dev/ttyUSB3 /dev/ttyUSB4
>```
>
>Maintenant il faut automatiser le lancement de la commande précédente
>via udev :
>
>``` {.bash}
>root@jeedom:# vi /etc/udev/rules.d99-usb_modeswitch.rules
>SUBSYSTEM=="usb", ATTRS{idVendor}=="1bbb", ATTRS{idProduct}=="f000", RUN+="/usr/sbin/usb_modeswitch -c /etc/usb_modeswitch.conf"
>```
>
>Sous jeedom dans le plugin sms_custom, il faut (dans mon cas) utiliser le "port
>sms_custom" suivant : /dev/ttyUSB3. En gros il faut essayer chaque port pour
>trouver le bon…​

> **Le démons sms_custom est bien démarré, mais vous ne recevez aucun sms_custom**
>
>Une des causes probables est la mauvaise configuration réseau. Dans
>"Général" &gt; "Configuration" &gt; "Administration" &gt;
>"Configuration réseaux", vérifier le contenu du champ "Adresse URL ou IP".
>
>Ce dernier ne doit pas être localhost ou 127.0.0.1 mais l’adresse IP de
>votre Jeedom ou son nom DNS.

> **En mode debug j’ai l’erreur "timeout" qui apparaît**
>
>Cette erreur arrive quand la clef ne répond pas dans les 10 secondes
>qui suivent une demande. Les causes connues peuvent être :
>
>-   incompatibilité de la clef GSM,
>
>-   problème avec la version du firmware de la clef.

> **Lors du démarrage en mode debug j’ai : "socket already in use"**
>
>Cela veut dire que le démon est démarré mais que Jeedom n’arrive pas
>à le stopper. Vous pouvez soit redémarrer tout le système, soit en
>SSH faire "killall -9 refxcmd.py".

> **Le démon refuse de démarrer**
>
>Essayez de le démarrer en mode debug pour voir l’erreur.

> **J’ai plusieurs port USB pour ma clef GSM alors que je n’en ai qu’une**
>
>C’est normal, pour une raison inconnue les clef GSM créent 2 (et
>même plus) ports USB au niveau système. Il suffit d’en choisir un,
>peut importe lequel.

> **Jeedom n’envoie plus et ne reçoit plus de sms_custom**
>
>Ceci arrive en général si la clef GSM n’arrive plus à se connecter
>au réseau. Essayer de la déplacer et de voir si ça revient au bout
>de quelques minutes.
