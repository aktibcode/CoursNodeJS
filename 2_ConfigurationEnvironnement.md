Chapitre : CONFIGURATION DE L'ENVIRONNEMENT


A-  Configuration de l'environnement local

    Pour configurer votre environnement pour Node.js, vous avez besoin des deux logiciels suivants disponibles sur votre ordinateur (a) l'éditeur de texte et (b) les installables binaires Node.js.


    A-1 : Editeur de texte

        Ceci sera utilisé pour taper votre programme. Parmi les exemples de quelques éditeurs, on peut citer le Bloc-notes de Windows, la commande Édition du système d'exploitation, Brief, Epsilon, EMACS et vim ou vi, ... ou simplement VSCode .

        Le nom et la version de l'éditeur de texte peuvent varier selon les systèmes d'exploitation. Par exemple, le Bloc-notes sera utilisé sous Windows, et vim ou vi peuvent être utilisés sous Windows ainsi que sous Linux ou UNIX.

        Les fichiers que vous créez avec votre éditeur sont appelés fichiers sources et contiennent le code source du programme. Les fichiers sources des programmes Node.js sont généralement nommés avec l'extension « .js ».

        Avant de commencer votre programmation, assurez-vous d'avoir un éditeur de texte en place et d'avoir suffisamment d'expérience pour écrire un programme informatique, l'enregistrer dans un fichier et enfin l'exécuter.

    A-2 : L'environnement d'execution de NodeJS

        Le code source écrit dans un fichier source est simplement du JavaScript. L'interpréteur Node.js sera utilisé pour interpréter et exécuter votre code JavaScript.

        La distribution Node.js est fournie sous forme de fichier binaire installable pour les systèmes d'exploitation SunOS, Linux, Mac OS X et Windows avec les architectures de processeur x86 32 bits et 64 bits (amd64).

        La section suivante vous guidera sur la façon d'installer la distribution binaire Node.js sur différents systèmes d'exploitation.

            https://i.imgur.com/3WWSyZv.png

    A-3 : Telecharger NodeJS 

        Téléchargez la dernière version LTS (Long Term Support) du fichier d'archive installable Node.js à partir de Téléchargements Node.js


B-  Installation sur UNIX/Linux/Mac OS X et SunOS

        En fonction de l'architecture de votre système d'exploitation, téléchargez et extrayez l'archive node-vx.xx-osname.tar.gz dans /tmp, puis déplacez les fichiers extraits dans le répertoire /usr/local/nodejs. Par exemple :

        $ cd /tmp
        $ wget http://nodejs.org/dist/v11.3.1/node-v11.3.1-linux-x64.tar.gz
        $ tar xvfz node-v11.3.1-linux-x64.tar.gz
        $ mkdir -p /usr/local/nodejs
        $ mv node-v11.3.1-linux-x64/* /usr/local/nodejs

    -   Ajoutez /usr/local/nodejs/bin à la variable d'environnement PATH.

        Système d'exploitation	       Sortir
        Linux	                       exporter PATH=$PATH:/usr/local/nodejs/bin
        Mac	                           exporter PATH=$PATH:/usr/local/nodejs/bin
        FreeBSD	                       exporter PATH=$PATH:/usr/local/nodejs/bin


C-  Installation sur Windows

    Utilisez le fichier MSI et suivez les instructions pour installer Node.js. Par défaut, le programme d'installation utilise la distribution Node.js dans C:\Program Files\nodejs. Le programme d'installation doit définir le répertoire C:\Program Files\nodejs\bin dans la variable d'environnement PATH de Windows. Redémarrez toutes les invites de commande ouvertes pour que la modification prenne effet.

    C-1 :   Verifier l'installation

        Pour vérifier que Node.js est installé sur votre machine, exécutez simplement la commande suivante :

        $ node -v

    C-2 :   Exécution d'un fichier

        -   Créez un fichier js nommé main.js sur votre machine (Windows ou Linux) contenant le code suivant.

            /* Hello, World! program in node.js */
            console.log("Hello, World!")

        -   Exécutez maintenant le fichier main.js à l’aide de l’interpréteur Node.js pour voir le résultat :

            $ node main.js

        -   Si tout se passe bien avec votre installation, cela devrait produire le résultat suivant :

            Hello, World!