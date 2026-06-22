# Linux hands-on exercises

## Partie 1: Les fichiers et les dossiers

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

## Partie 2: Le scripting

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

## Partie 3: Le réseau

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

## Partie 4: Les redirections et les pipes

### 4.0 But

Vous allez explorer la manière dont Linux gère les données textuelles à travers les flux standard : l'entrée (stdin, 0), la sortie standard (stdout, 1) et la sortie d'erreur (stderr, 2). Vous apprendrez à filtrer des résultats et à chaîner des commandes en utilisant des "pipes" (|) , ainsi qu'à isoler les messages d'erreur.

### 4.1 Recherche récursive de texte

1. Nous allons rechercher le nom actuel de votre machine dans tous les fichiers de configuration du système. Pour obtenir ce nom de manière dynamique, nous allons utiliser un "subshell" avec la syntaxe $(commande). Le système exécutera d'abord la commande hostname, puis remplacera $(hostname) par son résultat pour le fournir à grep.
L'option courte -r de grep permet d'effectuer cette recherche de manière récursive dans tous les sous-dossiers.

2. Lancez la recherche dans le dossier /etc :

   ```bash
   grep -r "$(hostname)" /etc
   ```

3. Observez les résultats. Notez que certains fichiers peuvent être protégés et que vous pourriez voir des messages d'erreur indiquant que vous n'avez pas la permission de les lire.

4. Vu que seul le nom des fichiers contenant le nom de votre machine vous intéresse, vous pouvez utiliser l'option -l de grep pour n'afficher que les noms de fichiers correspondants, sans afficher les lignes correspondantes.

   ```bash
   grep -rl "$(hostname)" /etc
   ```

### 4.2: Redirection de la sortie d'erreur

1. Lors de l'étape précédente, vous avez probablement vu apparaître de nombreux messages d'erreur. C'est normal : en tant qu'utilisateur standard, vous n'avez pas le droit de lire certains fichiers.
Ces erreurs sont envoyées dans le flux "stderr" (le descripteur numéro 2). Pour avoir un résultat propre, nous allons rediriger uniquement ces erreurs vers un fichier spécial nommé /dev/null, qui agit comme un trou noir supprimant tout ce qu'on y envoie. Le symbole 2> signifie "rediriger le flux d'erreur".

2. Relancez la commande en masquant les erreurs :

   ```bash
   grep -lr "$(hostname)" /etc 2>/dev/null
   ```

3. Observez les résultats. Vous devriez maintenant voir uniquement les lignes contenant le nom de votre machine, sans les messages d'erreur.

4. Bien sur, au lieu d'utiliser une redirection, vous pouvez demander à la commande grep d'ignorer les erreurs de permission en utilisant l'option -s (silent) :

   ```bash
   grep -slr "$(hostname)" /etc
   ```

### 4.3: Chaînage de commandes avec des pipes

1. Nous voulons maintenant lister tous les fichiers finissant par .log situés dans /var/log.
Nous allons utiliser la commande ls avec les options courtes -l (liste détaillée pour voir la date) et -t (pour trier par date décroissante). Ensuite, nous utiliserons le symbole pipe | pour connecter la sortie de cette commande ls directement dans l'entrée de la commande grep, qui filtrera uniquement les lignes contenant ".log".

   ```bash
   ls -lt /var/log | grep ".log"
   ```

2. Observez les résultats. Vous devriez voir une liste de fichiers .log triés par date, avec les détails de chaque fichier.

3. Vous pouvez voir que des fichiers qui ne terminent pas par .log sont aussi affichés, car ils contiennent ".log" dans leur nom (par exemple, "syslog.1"). C'est parce que grep recherche la chaîne ".log" n'importe où dans le nom du fichier, sur base d'une regexp (une expression régulière). Pour filtrer uniquement les fichiers qui finissent par .log, vous pouvez utiliser une expression régulière avec grep :

   ```bash
   ls -lt /var/log | grep "\.log$"
   ```

4. Vous pouvez aussi utiliser l'option -F de grep pour faire une recherche littérale sans interpréter les caractères spéciaux, et ainsi éviter d'avoir à échapper le point :

   ```bash
   ls -lt /var/log | grep -F ".log"
   ```

### 4.4 Sauvegarde du résultat

1. Pour garder une trace de cette recherche, nous allons rejouer la commande précédente en ajoutant une redirection standard (>) pour envoyer le résultat final dans un fichier texte nommé resultats_logs.txt

   ```bash
   ls -lt /var/log | grep -F ".log" > resultats_logs.txt
   ```

2. Vérifiez que le fichier resultats_logs.txt a été créé et affichez son contenu avec la commande cat :

   ```bash
   cat resultats_logs.txt
   ```

### 4.x Questions

1. Que fait la commande `grep -r` ?
2. Que fait la commande `grep -l` ?
3. Que fait la commande `2>/dev/null` ?
4. Que fait la commande `ls -lt` ?
5. Que fait la commande `grep -F` ?
6. Que fait la commande `>` pour rediriger la sortie d'une commande vers un fichier ? Comment faire pour ajouter du contenu à la fin du fichier au lieu de l'écraser ?

## Partie 5: Gestion des processus et signaux

### 5.0 But

L'objectif de cet exercice est de vous familiariser avec la gestion des processus et des signaux en Linux. Vous apprendrez à identifier les processus en cours d'exécution, à envoyer des signaux pour les contrôler, et à comprendre comment les processus réagissent à ces signaux.

### 5.1: Identifier les processus en cours d'exécution

1. Utilisez la commande `ps` pour afficher les processus en cours d'exécution sur votre machine.

   ```bash
   ps aux
   ```

2. Observez la liste des processus et notez les informations telles que le PID (Process ID), l'utilisateur, et la commande associée à chaque processus.

3. Filtrez la liste des processus pour n'afficher que ceux qui sont liés à systemd (le gestionnaire de services) en utilisant la commande `grep` :

   ```bash
   ps aux | grep systemd
   ```

4. Utilisez la commande `htop` pour afficher les processus en temps réel et observer l'utilisation des ressources par chaque processus.

   ```bash
   htop
   ```

### 5.2 : Envoyer des signaux à un processus

1. Choisissez un processus dans la liste que vous souhaitez contrôler (par exemple, un processus de votre terminal ou un processus de test que vous avez lancé). Notez son PID.

2. Utilisez la commande `kill` pour envoyer un signal de terminaison (SIGTERM) à ce processus en utilisant son PID :

   ```bash
   kill -15 <PID>
   ```

3. Vous pouvez également envoyer un signal de terminaison forcée (SIGKILL) à un processus en utilisant l'option -9. Attention, cela arrêtera immédiatement le processus sans lui donner la chance de se fermer proprement, pouvant mener à des pertes de données ou à des états incohérents :

   ```bash
   kill -9 <PID>
   ```

### 5.3 : Réagir aux signaux

1. Créez un script bash nommé `signal_test.sh` qui affiche un message lorsqu'il reçoit un signal de terminaison (SIGTERM). Le contenu du fichier devrait ressembler à ceci :

   ```bash
   #!/bin/bash

   # --- CONFIGURATION DES GESTIONNAIRES DE SIGNAUX (TRAPS) ---

   # Fonction exécutée en cas d'arrêt (Ctrl+C ou kill standard)
   fonction_quitter() {
      echo -e "\n[INTERRUPTION] Signal d'arrêt reçu !"
      echo "[INFO] Arrêt forcé de la commande en cours (PID du ping : $PING_PID)..."

      # On tue proprement le processus enfant (le ping)
      kill "$PING_PID" 2>/dev/null

      echo "[INFO] Nettoyage terminé. Script fermé proprement."
      exit 0
   }

   # Fonction personnalisée exécutée en cas de signal SIGUSR1
   fonction_statut() {
      echo -e "\n[STATUT] Signal SIGUSR1 reçu ! Tout va bien, le script tourne toujours."
      echo "[STATUT] La commande longue (ping) est active sous le PID : $PING_PID."
   }

   # Liaison des signaux aux fonctions correspondantes
   # SIGINT  = Ctrl+C
   # SIGTERM = Commande 'kill' par défaut
   # SIGUSR1 = Signal personnalisé pour l'utilisateur
   trap fonction_quitter SIGINT SIGTERM
   trap fonction_statut SIGUSR1

   # --- CORPS DU SCRIPT ---

   echo "========================================================="
   echo " Gestion des Signaux Bash"
   echo "========================================================="
   echo "Mon PID (Process ID) est : $$"
   echo "Pour envoyer un signal personnalisé : kill -SIGUSR1 $$"
   echo "Pour quitter proprement : Ctrl+C ou kill $$"
   echo "========================================================="
   echo "Lancement d'une commande longue (ping infini vers localhost)..."

   # Lancement de la commande en tâche de fond
   ping 127.0.0.1 > /dev/null &
   PING_PID=$! # On récupère le PID du ping

   # Le script attend la fin du processus enfant.
   # 'wait' a l'avantage d'être interrompu instantanément par les captures (traps).
   while kill -0 "$PING_PID" 2>/dev/null; do
      wait "$PING_PID"
   done

   echo "[INFO] Le processus enfant s'est terminé. Fin du script."
   ```

2. Rendez le script exécutable :

   ```bash
   chmod +x signal_test.sh
   ```

3. Exécutez le script dans un terminal. Le PID est donné dans le message de bienvenue du script :

   ```bash
   ./signal_test.sh
   ```

4. Pendant que le script est en cours d'exécution, ouvrez un autre terminal et envoyez un signal personnalisé (SIGUSR1) au script pour voir comment il réagit :

   ```bash
   kill -SIGUSR1 <PID_DU_SCRIPT>
   ```

5. Observez la sortie du script dans le premier terminal. Vous devriez voir le message indiquant que le signal SIGUSR1 a été reçu et que le script continue de fonctionner.

6. Lancez la commande suivante pour afficher les processus ping en cours, et leur parent.

   ```bash
   ps axo user,tty,pid,ppid,cmd | awk 'NR == 1 || /ping 127.0.0.1/'
   ```

7. Pour arrêter le script proprement, vous pouvez soit appuyer sur `Ctrl + C` dans le terminal où le script s'exécute, soit envoyer un signal de terminaison (SIGTERM) depuis un autre terminal :

   ```bash
   kill <PID_DU_SCRIPT>
   ```

8. Observez la sortie du script dans le premier terminal. Vous devriez voir le message indiquant que le signal de terminaison a été reçu et que le script a arrêté le processus enfant (le ping) avant de se fermer proprement.

9. Essayez d'envoyer un signal SIGKILL au script pour voir comment il réagit. Notez que le script ne pourra pas intercepter ce signal et sera immédiatement arrêté sans exécuter les fonctions de nettoyage.

   ```bash
   kill -9 <PID_DU_SCRIPT>
   ```

10. Essayez de chercher le process ping dans le terminal avec la commande `ps` pour vérifier si le processus ping est toujours actif après l'envoi du signal SIGKILL. Vous devriez constater que le processus ping existe toujours, car le script n'a pas eu l'occasion de le tuer proprement.

   ```bash
   ps axo user,tty,pid,ppid,cmd | awk 'NR == 1 || /ping 127.0.0.1/'
   ```

11. Notez que le parent n'est plus le script bash (qui a été tué), mais une instance du processus systemd dédiée à l'utilisateur (pas le process 1).

### 5.x Questions

1. Que fait la commande `ps aux` ?
2. Que fait la commande `htop` ?
3. Que fait la commande `kill -15 <PID>` ?
4. Que fait la commande `kill -9 <PID>` ?
5. Comment le script `signal_test.sh` gère-t-il les signaux SIGINT, SIGTERM et SIGUSR1 ? Que font les fonctions `fonction_quitter` et `fonction_statut` ?
6. Que se passe-t-il lorsque vous envoyez un signal SIGKILL au script ? Pourquoi le script ne peut-il pas intercepter ce signal ?
7. Que se passe-t-il avec le processus ping lorsque vous envoyez un signal SIGKILL au script ? Pourquoi ?
8. Comment vérifier que le processus ping est toujours actif après l'envoi du signal SIGKILL ? Quel est le parent de ce processus ping dans ce cas ?
