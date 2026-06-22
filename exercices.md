# Linux hands-on exercises

## Partie 1: Les fichiers et les dossiers

### 1.0: But

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

### 1.x: Questions

1. Que fait la commande `mkdir -p` ?
2. Que fait la commande `ls -R` ?
3. Que fait la commande `date > file` ?
4. Que fait la commande `file` ?

## Partie 2: Le scripting

### 2.0: But

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
   sudo nano /usr/local/bin/liste_fichiers.sh
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

   AFFICHER_LISTE=1
   AFFICHER_FICHIERS=1
   AFFICHER_DOSSIERS=1

   case "$1" in
   -s)
      AFFICHER_LISTE=0
      ;;
   -d)
      AFFICHER_FICHIERS=0
      AFFICHER_LISTE=0
      ;;
   *)
      if [[ -n $1 ]]; then
         help
      fi
      ;;
   esac

   if [[ $AFFICHER_LISTE -eq 1 ]]; then
      echo "Liste des fichiers dans le répertoire courant:"
      ls -l
   fi

   if [[ $AFFICHER_FICHIERS -eq 1 ]]; then
      echo "Nombre total de fichiers:"
      find . -maxdepth 1 -type f | wc -l
   fi

   if [[ $AFFICHER_DOSSIERS -eq 1 ]]; then
      echo "Nombre total de répertoires:"
      find . -maxdepth 1 -type d | wc -l
   fi
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
   sudo nano /usr/local/bin/liste_fichiers.sh
   ```

2. Modifiez le script pour qu'il utilise les subshells, et affiche le nombre de fichiers sur une seule ligne. Insérez les lignes suivantes dans le script existant:

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

   AFFICHER_LISTE=1
   AFFICHER_FICHIERS=1
   AFFICHER_DOSSIERS=1

   case "$1" in
   -s)
      AFFICHER_LISTE=0
      ;;
   -d)
      AFFICHER_FICHIERS=0
      AFFICHER_LISTE=0
      ;;
   *)
      if [[ -n $1 ]]; then
         help
      fi
      ;;
   esac

   if [[ $AFFICHER_LISTE -eq 1 ]]; then
      echo "Liste des fichiers dans le répertoire courant:"
      ls -l
   fi

   if [[ $AFFICHER_FICHIERS -eq 1 ]]; then
      FICHIERS=$(find . -maxdepth 1 -type f | wc -l)
      echo "Nombre total de fichiers: $FICHIERS"
   fi

   if [[ $AFFICHER_DOSSIERS -eq 1 ]]; then
      DOSSIERS=$(find . -maxdepth 1 -type d | wc -l)
      echo "Nombre total de répertoires: $DOSSIERS"
   fi
   ```

3. Enregistrez le fichier et quittez l'éditeur `nano`.

4. Exécutez le script sans options:

   ```bash
   liste_fichiers.sh
   ```

5. Vous devriez voir la liste des fichiers et des répertoires, ainsi que leur nombre total, s'afficher dans le terminal.

### 2.7: Créer un script qui affiche un message donné en argument autant de fois que demandé

1. Créez un nouveau fichier texte nommé `affiche_message.sh`:

   ```bash
   nano affiche_message.sh
   ```

2. Dans l'éditeur `nano`, écrivez un script bash qui prend deux arguments : un nombre et un message. Le script doit afficher le message autant de fois que le nombre spécifié. Le contenu du fichier devrait ressembler à ceci:

   ```bash
   #!/usr/bin/env bash

   function help {
       echo "Usage: $0 <nombre> <message>"
       exit 1
   }

   if [[ $# -lt 2 ]]; then
       help
   fi

   COUNT=$1
   shift

   MESSAGE="$*"

   for i in $(seq 1 "$COUNT"); do
       echo "$MESSAGE"
   done
   ```

3. Enregistrez le fichier et quittez l'éditeur `nano`.

4. Rendez le script exécutable:

   ```bash
   chmod +x affiche_message.sh
   ```

5. Appelez le script avec un nombre et un message en argument:

   ```bash
   ./affiche_message.sh 5 "Bonjour, Monde!"
   ```

### 2.x: Questions

1. Que fait la ligne `#!/usr/bin/env bash` au début de chaque script?
2. Comment renommer un fichier en utilisant la ligne de commande? Quelle différence avec un déplacement de fichier?
3. Que fait la commande `find . -maxdepth 1 -type f | wc -l` dans le script?
4. Comment le script gère-t-il les options `-s` et `-d`? Est-ce que les options peuvent être combinées?
5. Comment vérifier que `/usr/local/bin` est dans votre variable d'environnement `PATH`?

## Partie 3: Le réseau

### 3.0: But

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
3. Établissez une connexion vers un site web (voir 3.4, étape 1) et réexécutez la commande `ss` pour observer les changements.

    ```bash
    ss -tpn
    ```

4. Fermez la connexion établie et réexécutez la commande `ss` pour observer les changements.

    ```bash
    ss -tpn
    ```

### 3.x: Questions

1. Quelle est l'adresse IP de votre interface réseau principale ?
2. Quel est le temps de réponse lorsque vous pinguez Google ?
3. Quel est le temps de réponse lorsque vous pinguez votre gateway locale ?
4. Quelle est l'ordre de grandeur du temps de réponse entre le ping de Google et le ping de votre gateway locale ? Pourquoi ?
5. Quelle adresse IP est retournée lorsque vous résolvez le nom de domaine www.ifapme.be ?
6. Quelle est la réponse du serveur web lorsque vous demandez la page d'accueil de www.ifapme.be ?
7. Quelles informations utiles pouvez-vous obtenir en utilisant la commande `ss` pour afficher les connexions réseau actives ?

## Partie 4: Les redirections et les pipes

### 4.0: But

Vous allez explorer la manière dont Linux gère les données textuelles à travers les flux standard : l'entrée (stdin, 0), la sortie standard (stdout, 1) et la sortie d'erreur (stderr, 2). Vous apprendrez à filtrer des résultats et à chaîner des commandes en utilisant des "pipes" (|) , ainsi qu'à isoler les messages d'erreur.

### 4.1: Recherche récursive de texte

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

### 4.4: Sauvegarde du résultat

1. Pour garder une trace de cette recherche, nous allons rejouer la commande précédente en ajoutant une redirection standard (>) pour envoyer le résultat final dans un fichier texte nommé resultats_logs.txt

   ```bash
   ls -lt /var/log | grep -F ".log" > resultats_logs.txt
   ```

2. Vérifiez que le fichier resultats_logs.txt a été créé et affichez son contenu avec la commande cat :

   ```bash
   cat resultats_logs.txt
   ```

### 4.x: Questions

1. Que fait la commande `grep -r` ?
2. Que fait la commande `grep -l` ?
3. Que fait la commande `2>/dev/null` ?
4. Que fait la commande `ls -lt` ?
5. Que fait la commande `grep -F` ?
6. Que fait la commande `>` pour rediriger la sortie d'une commande vers un fichier ? Comment faire pour ajouter du contenu à la fin du fichier au lieu de l'écraser ?

## Partie 5: Gestion des processus et signaux

### 5.0: But

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

### 5.2: Envoyer des signaux à un processus

1. Choisissez un processus dans la liste que vous souhaitez contrôler (par exemple, un processus de votre terminal ou un processus de test que vous avez lancé). Notez son PID.

2. Utilisez la commande `kill` pour envoyer un signal de terminaison (SIGTERM) à ce processus en utilisant son PID :

   ```bash
   kill -15 <PID>
   ```

3. Vous pouvez également envoyer un signal de terminaison forcée (SIGKILL) à un processus en utilisant l'option -9. Attention, cela arrêtera immédiatement le processus sans lui donner la chance de se fermer proprement, pouvant mener à des pertes de données ou à des états incohérents :

   ```bash
   kill -9 <PID>
   ```

### 5.3: Réagir aux signaux

1. Créez un script bash nommé `signal_test.sh` qui affiche un message lorsqu'il reçoit un signal de terminaison (SIGTERM). Le contenu du fichier devrait ressembler à ceci :

   ```bash
   #!/usr/bin/env bash

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

### 5.x: Questions

1. Que fait la commande `ps aux` ?
2. Que fait la commande `htop` ?
3. Que fait la commande `kill -15 <PID>` ?
4. Que fait la commande `kill -9 <PID>` ?
5. Comment le script `signal_test.sh` gère-t-il les signaux SIGINT, SIGTERM et SIGUSR1 ? Que font les fonctions `fonction_quitter` et `fonction_statut` ?
6. Que se passe-t-il lorsque vous envoyez un signal SIGKILL au script ? Pourquoi le script ne peut-il pas intercepter ce signal ?
7. Que se passe-t-il avec le processus ping lorsque vous envoyez un signal SIGKILL au script ? Pourquoi ?
8. Comment vérifier que le processus ping est toujours actif après l'envoi du signal SIGKILL ? Quel est le parent de ce processus ping dans ce cas ?

## Partie 6: Automatisation avec systemd

### 6.0: But

Dans ce laboratoire, vous allez découvrir comment Linux gère l'automatisation moderne des tâches avec le gestionnaire systemd. Au lieu d'utiliser l'ancien planificateur cron , vous allez packager un script sous forme de service système, puis créer un "timer" pour l'exécuter de manière répétée

### 6.1: Créer un service systemd

1. Créez un script bash nommé `/usr/local/bin/mon_service.sh` (en mode sudo) qui affiche la date et l'heure actuelles dans un fichier de log à chaque exécution. Le contenu du fichier devrait ressembler à ceci :

   ```bash
   #!/usr/bin/env bash
   echo "Service exécuté à : $(date)" >> /var/log/mon_service.log
   ```

2. Rendez le script exécutable :

   ```bash
   sudo chmod +x /usr/local/bin/mon_service.sh
   ```

3. Créez un fichier de service systemd nommé `~/.config/systemd/user/mon_service.service` avec le contenu suivant :

   ```ini
   [Unit]
   Description=Mon Service de Log de Date

   [Service]
   Type=oneshot
   ExecStart=/usr/local/bin/mon_service.sh
   ```

4. Créez un fichier de timer systemd nommé `~/.config/systemd/user/mon_service.timer` avec le contenu suivant pour exécuter le service toutes les minutes :

   ```ini
   [Unit]
   Description=Timer pour Mon Service de Log de Date

   [Timer]
   OnCalendar=*-*-* *:*:00
   Persistent=true

   [Install]
   WantedBy=timers.target
   ```

5. Rechargez les unités systemd pour prendre en compte les nouveaux fichiers de service et de timer :

   ```bash
   systemctl --user daemon-reload
   ```

6. Activez le timer pour qu'il démarre automatiquement à chaque démarrage de session :

   ```bash
   systemctl --user enable mon_service.timer
   ```

7. Démarrez le timer pour qu'il commence à exécuter le service immédiatement :

   ```bash
   systemctl --user start mon_service.timer
   ```

8. Testez que le service fonctionne en le démarrant manuellement :

   ```bash
   systemctl --user start mon_service.service
   ```

9. Si le fichier n'existe pas déjà, le service va échouer, car il tourne en tant qu'utilisateur standard et n'a pas les permissions pour écrire dans /var/log. Créez le fichier de log avec les bonnes permissions pour permettre au service d'écrire dedans :

   ```bash
   sudo touch /var/log/mon_service.log
   sudo chmod 0666 /var/log/mon_service.log
   ```

10. Vérifiez que le service s'exécute correctement et que les entrées de log sont ajoutées à /var/log/mon_service.log :

    ```bash
    tail -f /var/log/mon_service.log
    ```

### 6.x: Questions

1. Que fait la section [Unit] dans un fichier de service systemd ?
2. Que fait la section [Service] dans un fichier de service systemd ?
3. Que fait la section [Timer] dans un fichier de timer systemd ?
4. Que fait la section [Install] dans un fichier de timer systemd ?
5. Que fait la commande `systemctl --user daemon-reload` ?
6. Que fait la commande `systemctl --user enable mon_service.timer` ?
7. Que fait la commande `systemctl --user start mon_service.timer` ?
8. Pourquoi le service échoue-t-il initialement lorsqu'il essaie d'écrire dans /var/log ? Comment résoudre ce problème ?
9. Comment vérifier que le service s'exécute correctement et que les entrées de log sont ajoutées à /var/log/mon_service.log ?
10. A quoi sert la directive `Persistent=true` dans la section [Timer] du fichier de timer systemd ?
11. A quoi sert l'option --user dans les commandes systemctl ? Quelle est la différence entre les services système et les services utilisateur dans systemd ?

## Partie 7: Gestion des utilisateurs, des groupes et des permissions

### 7.0: But

Linux est un système d'exploitation multi-utilisateurs. Pour garantir la sécurité, chaque fichier et répertoire appartient à un utilisateur (son propriétaire) et à un groupe. Dans ce laboratoire, vous allez apprendre à créer de nouveaux utilisateurs, à leur attribuer des mots de passe, et à manipuler les droits d'accès (lecture, écriture, exécution) pour bloquer l'accès à vos fichiers personnels.

### 7.1: Création d'un dossier partagé public

1. Créez un nouveau dossier nommé `public` dans le répertoire `/srv` :

   ```bash
   sudo mkdir /srv/public
   ```

2. Par défaut, ce dossier est protégé. Nous allons utiliser la commande chmod avec la notation octale pour lui donner les droits 0777. Cela signifie que le propriétaire (7), le groupe (7) et tous les autres utilisateurs (7) auront les droits de lecture (4) + écriture (2) + exécution (1). C'est un dossier totalement ouvert.

   ```bash
   sudo chmod 0777 /srv/public
   ```

3. Vérifiez les permissions du dossier avec la commande ls :

   ```bash
   ls -ld /srv/public
   ```

### 7.2: Vue d'ensemble des utilisateurs et création d'utilisateurs interactifs

1. Affichez la liste des utilisateurs existants sur votre système en consultant le fichier /etc/passwd :

   ```bash
   tail -n 5 /etc/passwd
   ```

2. N'affichez que les utilisateurs interactifs (ceux qui ont un shell valide) en utilisant la commande grep :

   ```bash
   grep -E '(/bin/bash|/bin/sh|/bin/zsh)$' /etc/passwd
   ```

3. Affichez la liste des utilisateurs qui ont un mot de passe défini (ceux dont le hash du mot de passe commence par $y$) en utilisant la commande awk pour filtrer le fichier /etc/shadow :

   ```bash
   sudo awk -F':' '$2 ~ /\$y.*/' /etc/shadow
   ```

### 7.3: Création des utilisateurs interactifs

1. Créez un nouvel utilisateur nommé `alice` avec la commande useradd. L'option -m crée automatiquement un répertoire personnel pour l'utilisateur.

   ```bash
   sudo useradd -m alice
   ```

2. Attribuez un mot de passe à l'utilisateur `alice` avec la commande passwd (mettez un mot de passe simple pour les besoins de l'exercice, par exemple "alice") :

   ```bash
   sudo passwd alice
   ```

3. Répétez les étapes 1 et 2 pour créer un autre utilisateur nommé `bob` avec le mot de passe "bob".

   ```bash
   sudo useradd -m bob
   sudo passwd bob
   ```

### 7.4: Création d'un groupe et ajout des utilisateurs

1. Créez un nouveau groupe nommé `groupe_partage` avec la commande groupadd :

   ```bash
   sudo groupadd groupe_partage
   ```

2. Ajoutez les utilisateurs `alice` et `bob` au groupe `groupe_partage` avec la commande usermod :

   ```bash
   sudo usermod -aG groupe_partage alice
   sudo usermod -aG groupe_partage bob
   ```

3. Vérifiez que les utilisateurs ont bien été ajoutés au groupe en utilisant la commande groups :

   ```bash
   groups alice
   groups bob
   ```

4. Changez le groupe propriétaire du dossier `/srv/public` pour qu'il appartienne au groupe `groupe_partage` avec la commande chown :

   ```bash
   sudo chgrp groupe_partage /srv/public
   ```

5. Changez les permissions du dossier `/srv/public` pour que le groupe ait les droits de lecture, écriture et exécution (7) et que les autres utilisateurs n'aient aucun droit (0). Cela signifie que seul le propriétaire et les membres du groupe pourront accéder au dossier.

   ```bash
   sudo chmod 0770 /srv/public
   ```

6. Vérifiez les permissions du dossier avec la commande ls :

   ```bash
   ls -ld /srv/public
   ```

### 7.5: Connexion et création d'un fichier

1. Connectez-vous en tant qu'utilisateur `alice` en utilisant la commande su :

   ```bash
   su - alice
   ```

2. Créez un fichier nommé `fichier_alice.txt` dans le dossier `/srv/public` et écrivez-y du texte :

   ```bash
   echo "Ceci est le fichier d'Alice." > /srv/public/fichier_alice.txt
   ```

3. Vérifiez que le fichier a été créé et affichez son contenu avec la commande cat :

   ```bash
   cat /srv/public/fichier_alice.txt
   ```

4. Déconnectez-vous de l'utilisateur `alice` en tapant `exit` ou CTRL+D.

   ```bash
   exit
   ```

5. Connectez-vous en tant qu'utilisateur `bob` en utilisant la commande su :

   ```bash
   su - bob
   ```

6. Essayez de lire le fichier créé par `alice` avec la commande cat :

   ```bash
   cat /srv/public/fichier_alice.txt
   ```

7. Essayez de modifier le fichier créé par `alice` avec la commande echo et redirection :

   ```bash
   echo "Bob a modifié le fichier." >> /srv/public/fichier_alice.txt
   ```

8. Vérifiez que le fichier a été modifié et affichez son contenu avec la commande cat :

   ```bash
   cat /srv/public/fichier_alice.txt
   ```

9. Créez un fichier secret à bob dans le répertoire `/srv/public` et vérifiez que `alice` ne peut pas le lire.

   ```bash
   echo "Ceci est le fichier secret de Bob." > /srv/public/fichier_bob.txt
   chmod 0600 /srv/public/fichier_bob.txt
   ```

10. Déconnectez-vous de l'utilisateur `bob` en tapant `exit` ou CTRL+D.

    ```bash
    exit
    ```

11. Connectez-vous à nouveau en tant qu'utilisateur `alice` et essayez de lire le fichier secret de ` bob` :

    ```bash
    su - alice
    cat /srv/public/fichier_bob.txt
    ```

12. Vous devriez recevoir un message d'erreur indiquant que l'accès est refusé, car le fichier appartient à `bob` et a des permissions restrictives (600).

### 7.x: Questions

1. Quelle est la différence entre les permissions 0777 et 0770 pour un dossier ?
2. Comment vérifier les permissions d'un fichier ou d'un dossier avec la commande `ls` ?
3. Que fait la commande `useradd -m` ?
4. Que fait la commande `passwd` ?
5. Que fait la commande `groupadd` ?
6. Que fait la commande `usermod -aG` ?
7. Que fait la commande `chgrp` ?
8. Que fait la commande `chmod` avec les permissions 0770 ?
9. Que se passe-t-il lorsque `bob` essaie de lire le fichier secret de `alice` ? Pourquoi ?
10. Que se passe-t-il lorsque `alice` essaie de lire le fichier secret de `bob` ? Pourquoi ?
11. Comment pouvez-vous vérifier à quel groupe appartient un utilisateur avec la commande `groups` ?
12. Pourquoi est-il important de gérer correctement les permissions et les groupes sur un système multi-utilisateurs ?

