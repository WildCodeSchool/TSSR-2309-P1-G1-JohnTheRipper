# Guide d'installation du logiciel John The Ripper

Vous êtes en possession d'un dossier crypté dont vous avez oublié le mot de passe ou vous êtes en entreprise et devez tester la force des mots de passe de votre service ?
Le logiciel John The Ripper est un logiciel open source qui vous permettra de réaliser vos tests de façon rapide et simple afin d'assurer votre sécurité et celle de vos collaborateurs. 

## Comment fonctionne John The Ripper ?

John the ripper réussit à trouver les mots de passe en comparant leur hash avec les hashs des mots de passe qu'il essaye afin de trouver une correspondance.
Le hachage de mot de passe est une pratique de sécurité des plus basiques qui consiste à brouiller les données en changeant ce mot de passe en une série de caractères unique : le hash. Ce hash peut être créé par différents algorithmes (comme MD5, SHA1, SHA56...). Heureusement, John The Ripper est capable de décrypter les hashs de nombreux algorithmes de hashage. Il est même possible de télécharger des extensions si un algorithme n'est pas reconnu.

## Choix techniques : 

Ce logiciel fonctionnant de façon similaire sur une multitude d'OS, dans ce guide, nous verrons les étapes d'installation du logiciel sur un système Ubuntu. Ubuntu est un OS libre d'accès et simple à utiliser, nous le recommandons pour une première prise en main. Il faudra l'adapter à vos besoins si vous décidez de changer d'OS par la suite.
Ce guide d'installation est créé à des fins spécifiques et s'applique ici uniquement à un système Ubuntu. Vous pouvez visiter le [site officiel](https://www.openwall.com/john/) pour plus de renseignements ou pour l'installation sur d'autres OS. 


## Pré-requis :

N'ayant pas de contrainte technique concernant l'utilisation du logiciel John the ripper, vous pouvez l'utiliser sans difficultées sur votre système Ubuntu. Toutefois pour l'installation de ce logiciel, il est nécessaire de connaître le système Ubuntu ainsi que l'utilisation de son terminal et ses commandes. 

# Étapes d'installation et de configuration : instruction étape par étape
_____________


### Installation d'un dossier partagé Windows-Linux
________

Le dossier étant sur une machine distante **windows**, il est nécessaire de réaliser les étapes suivante:

1- **Créer un Utilisateur sur le serveur Windows.** Il servira de point d'échange:  
  - Créer dans la session Administrateur un utilisateur supplémentaire.
  - Cocher seulement les cases: Le mot de passe n'expire jamais; et  la case L'utilisateur ne peut pas changer de mot de passe.
  - Quitter le session Administrateur et aller sur la session du nouvel utilisateur. Cela permet de l'activer et de vérifier l'exactitude du mot de passe.
  - Créer un Dossier _A_partager_ dans le disk C:\\.
    _Le reste peut se faire sur cette session mais vous devrez renseigner à chaque fois le code Administrateur, sinon rechanger de session._
  - Aller dans les propriétés du dossier _A_partager_ pour le partager.
  - Aller dans les propriétés de l'utilisateur; Donner les droits à l'utilisateur dans l'onglet _securité_ et accès au partage dans l'onglet _partage_
  - Pour la suite vous devez retenir: Le **nom d'utilisateur**, le **mot de passe**, le **nom du dossier** partagé et l'**adresse IP** du serveur.
    _Pour l'exemple: Adresse IP = **192.168.1.8**; Utilisateur = **Echange**; Mot de passe = **azerty1***; Dossier = **Towindows**_
    
2- **Configurer la machine Ubuntu:**
  - Ouvrir un terminal.
  
  - Installer le paquet cifs.
    ```bash
    sudo apt install cifs-utils
    ```
  - Créer un dossier qui servira de point de montage pour le partage.
    ```bash
    sudo mkdir /mnt/Towindows
    ```
  - Créer un fichier qui contiendra les références nécessaires à l'échange. Il est préférable de le créer dans un autre endroit que le point de montage, dans le home par exemple.
    _Pour l'exemple : fichier = **references**._
    ```bash
    touch references
    ```
  - Rentrer les références dans le fichier _references_ et y donner l'accès uniquement à l'utilisateur.
    ```bash
    echo -e "username=Echange\npassword=azerty1*" > references
    sudo chmod 600 references
    ```
    
3- **Montage du partage avec Windows:**  
  - Pour monter le dossier :
    ```bash
    sudo mount -t cifs //192.168.1.8/Echange /mnt/Towindows/ -o credentials=/home/references
    ```
    Il est possible de remplacer l'adresse IP par le nom du serveur en renseignant le dossier /etc/hosts.
  - Pour démonter le dossier faire:
    ```bash
    sudo umount -t cifs //192.168.1.8/Echange /mnt/Towindows/
    ```
  - Pour le montage automatique du dossier de partage:
    Copier le fichier references dans /home/references. Cela permettra au lancement automatique d'avoir les références nécessaires à chaque démarrage et de pouvoir supprimer le 
    fichier s'il était sur le bureau par exemple.
    Éditer le dossier /etc/fstab:
    ```bash
    sudo nano /etc/fstab
    ```
    Une fois dans l'éditeur écrire:
    ```bash
    //192.168.1.8/Echanges /mnt/Towindows cifs credentials=/home/references,uid=1000,gid=1000 0       0
    ```
  - Pour tester la configuration du  montage faire:
    ```bash
    sudo mount -a
    ```
  - Relancer la machine en faisant:
    ```bash
    sudo reboot
    ```

_____________

### Installation du logiciel John the ripper.
___________


Ce logiciel peut être installé sur Ubuntu dans votre terminal en utilisant apt-get ou snap.  
Cependant, vous pouvez rencontrer des dysfonctionnements en l'installant avec la commande suivante :  
_sudo apt-get install john -y_.  
Nous recommandons donc de procéder avec l'installation snap. Le format snap permet l'installation de logiciels séparés du reste du système d'exploitation grâce à des mécanismes de sécurité. Il peut toutefois échanger du contenu en suivant certaines règles précises instaurées par l'administrateur.

1- Snap est normalement nativement installé sur votre Ubuntu. Si toutefois ce n'était pas le cas, vous pouvez l'installer avec la commande suivante : 

  ```bash
  sudo apt update
  sudo apt install snap
  ```  

  Votre terminal vous affichera le message suivant validant la bonne installation du programme.

  ![Image 2 ](https://github.com/ThomasDominici/Projet-BVT-1/blob/main/Ressources/Screenshots%20installation/1.5.JPG)


2- Vous pouvez maintenant lancer l'installation de John The Ripper par snap grâce à la commande suivante :     
  ```Bash
  sudo snap install john-the-ripper
  ```

  Un fois l'installation terminée, votre terminal affichera le message dans la photo suivante : 

  ![Image 4](https://github.com/ThomasDominici/Projet-BVT-1/blob/main/Ressources/Screenshots%20installation/3.JPG)

3- Taper maintenant _john_ dans votre terminal, il affiche le message suivant :

  ```Bash
  john
  ```

  ![Image 5](https://github.com/ThomasDominici/Projet-BVT-1/blob/main/Ressources/Screenshots%20installation/4.JPG)

  Nous pouvons voir la version du logiciel (ici 1.9.0).
  La ligne **usage** montre que nous pouvons fournir à John un fichier contenant une liste de mots de passe ainsi que choisir l'option avec laquelle il va tenter de déchiffrer les       fichiers que nous lui indiquerons.

  Voici quelques exemples d'options envisageables pour John : 

  1. **--single** : mode par défaut, John tente des combinaisons variables en fonction du nom de l'utilisateur.
  2. **--wordlist** : l'attaque par dictionnaire. John utilise une liste de mots de passe fournis afin de craquer le mot de passe du fichier désigné.
  3. **--incremental** : brut force, john teste toutes les combinaisons de caractères jusqu’à trouver le mot de passe. Infaillible en théorie mais peut prendre du temps en fonction de   la force du mot de passe du fichier sélectionné.

4- Nous allons maintenant créer des alias afin de pouvoir effectuer nos commandes plus rapidement : 
  ```Bash
  sudo snap alias john-the-ripper.zip2john zip2john 
  sudo snap alias john-the-ripper.keepass2john keepass2john 
  ```
Si besoin:
**Pour désinstaller :**

```bash
sudo snap remove john-the-ripper
```

________


## Difficultés rencontrées et solutions : 
  

| **Difficultées**   |     **Solutions**   |
|:-------------------|--------------------:|
| Logiciel peu efficace avec le paquet apt|  Installation du paquet avec snap|
| Capacité  de base limitée en liste de mots | Installation d'un paquet de liste supplémentaire openssl|
| Commandes peu intuitives |  Création d'alias pour les outils (zip2john et keypass2john).|
| Accéder aux dossier du serveur par la machine client| Utiliser un utilisateur windows servant aux échanges et installer l'outils cifs sur Ubuntu|

____

## Tests réalisés :

- Utilisation de John the ripper sur un dossier zip en mode simple sur une machine Ubuntu.
- Utilisation de John the ripper avec l'outil zip2john sur un dossier zip en mode dictionnaire sur une machine Ubuntu.
- Création d'un dossier partagé entre les deux machines virtuelles Windows Server 2022 (serveur) et Ubuntu (client).
- Récupération d'un fichier protégé sur la machine Ubuntu venant du serveur Windows

  
# Résultats obtenus : ce qui a fonctionné  
- L'utilisation en mode simple du logiciel sur un dossier local protégé à permis la récupération du mot de passe.
- l'utilisation en mode dictionnaire du logiciel sur un dossier local protégé à permis la récupération du mot de passe.
- Le montage d'un dossier de partage entre le client et le serveur à permis les échanges de dossier entre les deux machines.
- Le montage automatique du partage à permis les échanges sans avoir à refaire le montage à chaque utilisation.
- L'utilisation en mode simple du logiciel sur un dossier partagé et protégé à permis la récupération du mot de passe.
- L'utilisation en mode dictionnaire du logiciel sur un dossier partagé et protégé à permis la récupération du mot de passe.




