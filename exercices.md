# Linux hands-on exercises

## Partie 1

### 1.0 But

Dans cet exercice, vous allez apprendre à manipuler des dossiers et des fichiers en ligne de commande. Vous verrez également comment rediriger le résultat d'une commande dans un fichier et comment vérifier la nature d'un fichier, car sous Linux, tout est un fichier.

### 1.1: Création de l'arborescence de répertoires

1. Nous devons d'abord créer notre structure de dossiers. La commande mkdir permet de créer un nouveau dossier. Nous utilisons l'option courte -p qui est très pratique : elle crée également les dossiers parents nécessaires s'ils n'existent pas encore. Cela évite de taper une commande pour chaque niveau de répertoire.

   ```bash
   mkdir -p dir1/subdir1 dir2/subdir1
   ```

2. Vérifiez que les dossiers ont été créés en utilisant la commande ls qui liste le contenu d'un répertoire.

   ```bash
   ls -R
   ```

3. Pour connaitre l'utilité de l'option -R, utilisez la commande man pour afficher le manuel de la commande ls.

   ```bash
   man ls
   ```

4. Dans le manuel, cherchez la section "DESCRIPTION" et trouvez la description de l'option -R. Que fait-elle ? Vous pouvez aussi rechercher avec la touche `/` dans le manuel pour trouver rapidement l'information.

   ```bash
   /-R
   ```

### 1.2: Inscription de la date dans les fichiers

1. La consigne demande d'inscrire la date actuelle dans un fichier nommé file à l'intérieur de chaque sous-dossier. La commande date génère la date et affiche son résultat sur la sortie standard (l'écran). Pour inscrire ce résultat dans un fichier, nous utilisons l'opérateur de redirection `>` qui redirige la sortie standard vers un fichier, en écrasant son contenu s'il existait déjà.

   ```bash
   date > dir1/subdir1/file
   date > dir2/subdir1/file
   ```

2. Vérifiez que les fichiers ont été créés et que la date y est inscrite en utilisant la commande cat qui affiche le contenu d'un fichier.

   ```bash
   cat dir1/subdir1/file
   cat dir2/subdir1/file
   ```


### 1.3: Vérification de la nature d'un fichier

1. La commande file permet de vérifier la nature d'un fichier. Utilisez-la pour vérifier le type du fichier que vous venez de créer.

   ```bash
   file dir1/subdir1/file
   ```

### 1.x Questions

1. Que fait la commande `mkdir -p` ?
2. Que fait la commande `ls -R` ?
3. Que fait la commande `date > file` ?
4. Que fait la commande `file` ?
5. Que se passe-t-il si vous utilisez `>` pour rediriger la sortie d'une commande vers un fichier qui existe déjà ? Comment faire pour ajouter du contenu à la fin du fichier au lieu de l'écraser ?

## Partie 2

### 2.0 But

L'objectif de cet exercice est de se familiariser avec les bases de bash, du script shell et des commandes Linux.

### 2.1: Écrire et exécuter un script bash simple

1. Ouvrez un terminal sur votre machine Linux
2. Créez un nouveau fichier texte nommé `mon_script.sh` en utilisant la commande `nano`:

   ```bash
   nano mon_script.sh
   ```

3. Dans l'éditeur `nano`, écrivez un script bash simple qui affiche "Bonjour, Monde!" à l'écran. Le contenu du fichier devrait ressembler à ceci:

    ```bash
    #!/usr/bin/env bash
    echo "Bonjour, Monde!"
    ```

4. Enregistrez le fichier et quittez l'éditeur `nano` (appuyez sur `CTRL + X`, puis `Y`, puis `ENTER`).
5. Rendez le script exécutable en utilisant la commande `chmod`:

   ```bash
   chmod +x mon_script.sh
   ```

6. Exécutez le script en utilisant la commande suivante:

   ```bash
   ./mon_script.sh
   ```

7. Vous devriez voir "Bonjour, Monde!" s'afficher dans le terminal.

### 2.2: Rendre le script disponible globalement

1. Déplacez le script `mon_script.sh` dans un répertoire qui est inclus dans votre variable d'environnement `PATH`, comme `/usr/local/bin`:

   ```bash
   sudo mv mon_script.sh /usr/local/bin/
   ```

2. Maintenant, vous pouvez exécuter le script de n'importe où dans le terminal en tapant simplement:

   ```bash
   mon_script.sh
   ```

3. Vous devriez toujours voir "Bonjour, Monde!" s'afficher dans le terminal, peu importe votre répertoire actuel.

4. Le script est disponible globalement parce que le répertoire `/usr/local/bin` est inclus dans la variable d'environnement `PATH`, qui est une liste de répertoires que le système recherche pour trouver des exécutables. En déplaçant le script dans ce répertoire, vous permettez au système de le trouver et de l'exécuter depuis n'importe où.

   ```bash
   echo $PATH
   ```

### 2.3: Écrire un script bash avec des arguments

1. Créez un nouveau fichier texte nommé `salutation.sh`:

   ```bash
   nano salutation.sh
   ```

2. Dans l'éditeur `nano`, écrivez un script bash qui prend un argument (un nom) et affiche "Bonjour, [nom]!" à l'écran. Le contenu du fichier devrait ressembler à ceci:

   ```bash
   #!/usr/bin/env bash
   if [[ $# -eq 0 ]]; then
       echo "Usage: $0 <nom>"
       exit 1
   fi
   echo "Bonjour, $1!"
   ```

3. Enregistrez le fichier et quittez l'éditeur `nano`.
4. Rendez le script exécutable:

   ```bash
   chmod +x salutation.sh
   ```

5. Déplacez le script dans `/usr/local/bin`:

   ```bash
   sudo mv salutation.sh /usr/local/bin/
   ```

6. Exécutez le script avec un argument:

   ```bash
   salutation.sh Alice
   ```

7. Vous devriez voir "Bonjour, Alice!" s'afficher dans le terminal.

### 2.4: Utiliser des commandes Linux dans un script bash

1. Créez un nouveau fichier texte nommé `liste_fichiers.sh`:

   ```bash
   nano liste_fichiers.sh
   ```

2. Dans l'éditeur `nano`, écrivez un script bash qui liste tous les fichiers dans le répertoire courant et affiche le nombre total de fichiers. Le contenu du fichier devrait ressembler à ceci:

   ```bash
   #!/usr/bin/env bash
   echo "Liste des fichiers dans le répertoire courant:"
   ls -l
   echo "Nombre total de fichiers:"
   find . -maxdepth 1 -type f | wc -l
   echo "Nombre total de répertoires:"
   find . -maxdepth 1 -type d | wc -l
   ```

3. Enregistrez le fichier et quittez l'éditeur `nano`.
4. Rendez le script exécutable:

   ```bash
   chmod +x liste_fichiers.sh
   ```

5. Déplacez le script dans `/usr/local/bin`:

   ```bash
   sudo mv liste_fichiers.sh /usr/local/bin/
   ```

6. Exécutez le script:

   ```bash
   liste_fichiers.sh
   ```

7. Vous devriez voir la liste des fichiers et des répertoires, ainsi que leur nombre total, s'afficher dans le terminal.

### 2.5: Modifier le script de la partie 4 pour inclure des options

1. Ouvrez le fichier `liste_fichiers.sh` dans un éditeur de texte:

   ```bash
   nano /usr/local/bin/liste_fichiers.sh
   ```

2. Modifiez le script pour qu'il accepte une option `-s` qui, si elle est fournie, n'affiche pas la liste des fichiers mais seulement le nombre total de fichiers, et une option `-d` qui affiche seulement le nombre total de répertoires. Le contenu modifié du fichier devrait ressembler à ceci:

   ```bash
   #!/usr/bin/env bash

   function help {
       echo "Usage: $0 [-s] [-d]"
       echo "  -s    Affiche seulement le nombre total de fichiers"
       echo "  -d    Affiche seulement le nombre total de répertoires"
       exit 1
   }

    if [[ $# -gt 1 ]]; then
        help
    fi

    if [[ $1 == "-d" ]]; then
        DOSSIERS_UNIQUEMENT=1
    elif [[ $1 == "-s" ]]; then
        AFFICHER_LISTE=0
    else
        help
    fi

    if [[ $AFFICHER_LISTE -ne 0 ]]; then
        echo "Liste des fichiers dans le répertoire courant:"
        ls -l
    fi

    if [[ $DOSSIERS_UNIQUEMENT -ne 1 ]]; then
        echo "Nombre total de fichiers:"
        find . -maxdepth 1 -type f | wc -l
    fi

    echo "Nombre total de répertoires:"
    find . -maxdepth 1 -type d | wc -l
   ```

3. Enregistrez le fichier et quittez l'éditeur `nano`.

4. Exécutez le script avec l'option `-d`:

   ```bash
   liste_fichiers.sh -d
   ```

5. Vous devriez voir la liste des répertoires et leur nombre total s'afficher dans le terminal.

6. Exécutez le script avec l'option `-s`:

   ```bash
   liste_fichiers.sh -s
   ```

7. Vous devriez voir le nombre total des fichiers et dossiers s'afficher dans le terminal.

### 2.6: Modifier le script de la partie 5 pour y modifier le comportement

1. Ouvrez le fichier `liste_fichiers.sh` dans un éditeur de texte:

   ```bash
   nano /usr/local/bin/liste_fichiers.sh
   ```

2. Modifiez le script pour qu'il utilise les subshells, et affiche le nombre de fichiers sur une seule ligne. Insérez les lignes suivantes dans le script existant:

   ```bash
    FICHIERS=$(find . -maxdepth 1 -type f | wc -l)
    DOSSIERS=$(find . -maxdepth 1 -type d | wc -l)
    echo "Nombre total de fichiers: $FICHIERS"
    echo "Nombre total de répertoires: $DOSSIERS"
   ```

3. Enregistrez le fichier et quittez l'éditeur `nano`.
4. Exécutez le script sans options:

   ```bash
   liste_fichiers.sh
   ```

5. Vous devriez voir la liste des fichiers et des répertoires, ainsi que leur nombre total, s'afficher dans le terminal.

### 2.x Questions

1. Que fait la ligne `#!/usr/bin/env bash` au début de chaque script?

2. Comment renommer un fichier en utilisant la ligne de commande? Quelle différence avec un déplacement de fichier?

3. Que fait la commande `find . -maxdepth 1 -type f | wc -l` dans le script?

4. Comment le script gère-t-il les options `-s` et `-d`? Est-ce que les options peuvent être combinées?

5. Comment vérifier que `/usr/local/bin` est dans votre variable d'environnement `PATH`?

## Partie 3

### 3.0 But

L'objectif de cet exercice est de vous familiariser avec les bases du réseau en Linux.

### 3.1: Découverte des commandes réseau

1. Ouvrez un terminal sur votre machine Linux.
2. Utilisez la commande `ip` pour afficher les informations sur les interfaces réseau de votre machine.

    ```bash
    ip address show
    ip addr
    ip a
    ```

3. Notez l'adresse IP de votre interface réseau principale (généralement `eth0` ou `wlan0`).

### 3.2: Ping

1. Utilisez la commande `ping` pour tester la connectivité avec un autre hôte sur le réseau. Par exemple, vous pouvez pinguer Google :

    ```bash
    ping google.com
    ```

2. Observez les résultats et notez le temps de réponse.
3. Arrêtez le ping en appuyant sur `Ctrl + C`.
4. Essayez de pinguer une adresse IP locale (par exemple, l'adresse IP de votre gateway). Trouvez cette adresse en utilisant la commande `ip route`.

    ```bash
    ip route
    ```

5. Notez l'adresse IP de la gateway (l'entrée 'default via ...').
6. Pinguez cette adresse IP locale et observez les résultats. Quelle est l'ordre de grandeur du temps de réponse par rapport au ping de Google ?
7. Essayez de pinguer une adresse IP instable, comme 106.15.195.14, et observez les résultats.
8. Essayez de pinguer une adresse IP non routable, comme 1.1.2.3, et observez les résultats.

### 3.3: DNS

1. Utilisez la commande `dig` pour résoudre un nom de domaine en adresse IP

    ```bash
    dig www.ifapme.be
    ```

2. Notez l'adresse IP retournée par la commande (section "ANSWER SECTION").

### 3.4: Connexions réseau

1. Utilisez la commande `nc` pour ouvrir une connexion TCP vers un serveur web (par exemple, `www.ifapme.be` sur le port 80).

    ```bash
    nc www.ifapme.be 80
    ```

2. Une fois connecté, tapez la commande HTTP suivante pour demander la page d'accueil :

    ```bash
    GET / HTTP/1.1
    Host: www.ifapme.be
    ```

3. Appuyez sur `ENTER` deux fois pour envoyer la requête.
4. Observez la réponse du serveur web.

### 3.5: Afficher les connexions réseau actives

1. Utilisez la commande `ss` pour afficher les connexions réseau actives sur votre machine.

    ```bash
    ss -tpn
    ```

2. Notez les connexions établies.
3. Établissez une connexion vers un site web (voir 2.4, étape 1) et réexécutez la commande `ss` pour observer les changements.

    ```bash
    ss -tpn
    ```

4. Fermez la connexion établie et réexécutez la commande `ss` pour observer les changements.

    ```bash
    ss -tpn
    ```

### 3.x Questions

1. Quelle est l'adresse IP de votre interface réseau principale ?
2. Quel est le temps de réponse lorsque vous pinguez Google ?
3. Quel est le temps de réponse lorsque vous pinguez votre gateway locale ?
4. Quelle est l'ordre de grandeur du temps de réponse entre le ping de Google et le ping de votre gateway locale ? Pourquoi ?
5. Quelle adresse IP est retournée lorsque vous résolvez le nom de domaine www.ifapme.be ?
6. Quelle est la réponse du serveur web lorsque vous demandez la page d'accueil de www.ifapme.be ?
7. Quelles informations utiles pouvez-vous obtenir en utilisant la commande `ss` pour afficher les connexions réseau actives ?

## Partie 4

