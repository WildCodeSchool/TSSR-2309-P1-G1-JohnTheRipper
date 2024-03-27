# **Projet John The Ripper**
____
## **Le projet**

Le projet réalisé permet de tester  le logiciel [_**John The Ripper**_](https://www.openwall.com/john/) à partir d'un poste client. Il sert à testé la robustesse des mot de passe d'un serveur en utilisant une attaque par _dictionnaire_. 
### **John The Ripper c'est quoi?**
* #### **Son usage:**
> C'est un logiciel de cassage de mot de passe afin de tester l'efficacité de ceux-ci.
* #### **Ses possibilitées:**
>John The Ripper fonctionne aussi avec des options, les plus courantes sont le mode simple (essai des mots de passe en détournant le nom d'utlisateur), dictionnaire (utilise une wordlist en y détournant également le nom d'utilisateur) et le mode brute force ou incrémental (il essaye toutes les combinaisons de caractères possibles, jusqu'à trouver le mot de passe).
* #### **Ses capacités:**
>John The Ripper est capable d'attaquer les mots de passe hachés avec différentes fonctions de hachage, notamment les algorithmes les plus basiques comme MD5, Blowfish, Kerberos, AFS, et les LM hashes de Windows. Il est possible de rajouter des modules afin de lui permettre de décrypter des mots de passe basés sur les hash MD4, MySQL ou LDAP par exemple.
___

## **Les membres du groupe et leurs rôles**

|              |      **Sprint 1**      |     **Sprint 2**     |
|:--------------:|:-----------------------:|:---------------------:|
| **Valentin**   | Rechercher et renseigner les informations sur John The Ripper, possibilitées, objectifs, capacitées et usages de celui-ci.| _Product owner_: A du rendre compte au client de façon à garder le cap de l'avancement. Installer et utiliser John The Ripper et établir le guide d'utilisation.|
| **Thomas**   | _Product Owner_:  Maintenir la direction du projet. Monter les machines virtuelles choisies en réseaux interne. Synthétiser l'avancement de la semaine.| _Scrum master_: Assurer la coordination et les conditions de travail. Rédiger le readme du projet et le guide d'installation. Monter et présenter la démonstration de John The Ripper.|
| **Bilal**   | _Scrum Master_: Assurer la coordination et les bonnes conditions de travail. Définir les choix techniques. Installer le logiciel sur une VM| Monter le point de montage pour le dossier partagé entre les machines et intégrer le processus dans le guide d'installlation. Rédaction du Readme avec Thomas.| 
| **Commun** | Mise au point de la première présentation. Recherche d'informations d'utilisation et d'installation du logiciel. Test du logiciel sur un dossier.| Élaboration de la présentation. Test du logiciel sur un dossier partagé en provenance du serveur Windows|

_____


## **Choix techniques**
* **Machine client:**
John the ripper fonctionnant sur tout les OS courants, n'a pas de pré-requis quelconque, le choix s'est porté sur une distribution Ubuntu. La distribution Kali Linux serait la  plus appropriée car elle dispose de John the ripper nativement et des modules nécessaires à son utilisation. Cependant étant une machine trop spécifique nous gardons la Ubuntu qui est plus commune.
* **Machine server:**
La machine server est une Windows Server 2022. Ce choix a été pris afin de réaliser le projet sur 2 OS différents.
* **Type d'attaque:**
L'attaque se fera par le mode dictionnaire et devra tester l'efficacité du mot de passe d'un dossier zip protégé. Le dossier sera sur le serveur et le logiciel éxécuté depuis le poste client.

_____

## **Difficultés et solutions rencontrées:**

| **Difficultées**   |     **Solutions**   |
|:-------------------|--------------------:|
| Logiciel peu efficace avec le paquet apt|  Installation du paquet avec snap|
| Capacité  de base limitée en liste de mots | Installation d'un paquet de liste supplémentaire openssl|
| Commandes peu intuitives |  Création d'alias pour les outils (zip2john et keypass2john).|
| Accéder aux dossier du serveur par la machine client| Créer un point de montage d'échange sur Ubuntu et un utilisateur de partage sur le serveur.|

____

## **Tests:**

- Utilisation de John The Ripper sur un dossier zip en mode simple sur une machine Ubuntu.
- Utilisation de John The Ripper avec l'outil zip2john sur un dossier zip en mode dictionnaire sur une machine Ubuntu.
- Utilisation du logiciel sur un dossier ZIP en provenance de Windows server sur la machine Ubuntu.
- Tester le montage automatique du point de montage d'échange sur la machine Ubuntu.
