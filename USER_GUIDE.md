# Guide d'utilisation John The Ripper

## John The Ripper
C'est un logiciel libre de crackage de mots de passe .

## Utilisation de base
Pour utiliser **John The Ripper** il nous faut un dossier compressé sécurisé que l'ont peut créer en zip ou rar entre autre (pour notre présentation ça sera zip).

Pour facilité l'utilisation de **John The Ripper** nous allons commencer par créer des alias avec la commande :

```Bash
sudo snap alias john-the-ripper.zip2john zip2john
```

```Bash
sudo snap alias john-the-ripper.keepass2john keepass2john
```

Nous allons ensuite lancer **John The Ripper** sur le dossier ciblé en redirigeant la sortie dans un fichier texte pour recupérer le hash du mot de passe avec la commande :

```Bash
zip2john /home/user/Bureau/dossier-cible.zip > hash.txt
```

Une fois le _hash_ récuperé, il nous reste simplement à le décrypter en utilisant la commande :

```Bash
john hash.txt
```

Le terminal affichera alors le mot de passe du fichier.  

## Utilisation avancé

Dans les fonctions avancées nous allons tester l'attaque par _dictionnaire_ .

### L'attaque par dictionnaire

Pour ce faire, il nous faut une liste de mots de passe que l'ont peut télécharger sur [ openwall ](https://www.openwall.com/john/) ou ailleurs.
Nous utiliserons ici la liste **password.txt** qui contient 3000 mots de passe. Certaines listes sont bien plus complètes et contiennent plusieurs millions de mots.

Les premières étapes sont les mêmes que pour la méthode simple. On commence par récupérer le _hash_ du fichier cible , une fois fait on lance **john** mais cette fois avec l'attaque par dictionnaire. Pour ce faire on utilise la commande :

```Bash
john -w= /home/user/Bureau/password.lst hash.txt
```

Une fois le _hash_ récupéré nous utiliserons la commande suivante pour le décrypter et l'afficher :

```Bash
john --show hash.txt
```

Cela va nous permettre d'afficher le mot de passe plutôt que de l'envoyer dans un dossier.

Et voila le travail !

Pour voir toutes les options disponibles avec **john** vous pouvez tapez la commande suivante :

```Bash
john
```

Ce qui nous permettras d'afficher dans le terminal toutes les fonctions disponibles .

## Dépannage

#### Les problèmes courants :

- **John** ne trouve pas le dossier demandé ou la wordlist ?

  Pour résoudre ce problème il suffit bien souvent de vérifier le chemin d'accès .

- En tapant _zip2john_ le terminal affiche commande introuvable ?

  Vérifier que les alias ont été correctement créés .

 Voila les problèmes les plus courants toutefois pour des information plus detaillées, il est conseillé de se rendre sur le [ site officiel ]( https://www.openwall.com/john/).
