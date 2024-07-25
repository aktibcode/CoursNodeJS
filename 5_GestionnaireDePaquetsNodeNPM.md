Chapitre : GESTIONNAIRE DE PAQUETS NODE NPM

A-  Installation de modules à l'aide de npm

    Node Package Manager (NPM) fournit deux fonctionnalités principales :

    *   Les référentiels en ligne pour les packages/modules node.js, qui sont consultables, peuvent être trouvés ici Lien
    *   Utilitaire de ligne de commande pour installer les packages Node.js, effectuer la gestion des versions et la gestion des dépendances des packages Node.js.

    NPM est fourni avec les installables Node.js après la version v0.6.3. Pour vérifier la version, ouvrez la console et saisissez la commande suivante et voyez le résultat :

        $ npm --version
        6.13.4

    Si vous utilisez une ancienne version de NPM, il est assez facile de la mettre à jour vers la dernière version. Utilisez simplement la commande suivante depuis la racine :

        $ npm install npm -g

    Il existe une syntaxe simple pour installer n'importe quel module Node.js :

        $ npm install <Module Name>

    Par exemple, voici la commande permettant d'installer un célèbre module de framework Web Node.js appelé Express :

        $ npm install express

    Vous pouvez maintenant utiliser ce module dans votre fichier .js comme suit :

        var express = require('express');

B-  Installation locale ou globale

    Par défaut, NPM installe toute dépendance en mode local. Ici, le mode local fait référence à l'installation du package dans le node_modulesrépertoire se trouvant dans le dossier où l'application Node est présente. Les packages déployés localement sont accessibles via require()la méthode.

    Par exemple, lorsque nous avons installé le module express, il a créé le répertoire node_modules dans le répertoire actuel où il a installé le module express.

    Alternativement, vous pouvez utiliser npm lsla commande pour répertorier tous les modules installés localement.

    Les packages/dépendances installés globalement sont stockés dans un répertoire système. Ces dépendances peuvent être utilisées dans la fonction CLI (Command Line Interface) de n'importe quel Node.js mais ne peuvent pas être importées require() directement à l'aide d'une application Node. Essayons maintenant d'installer le module Express à l'aide de l'installation globale.

        $ npm install express -g

    Cela produira un résultat similaire mais le module sera installé globalement. Ici, la première ligne indique la version du module et l'emplacement où il est installé.

    express@4.12.2 /usr/lib/node_modules/express
    ├── merge-descriptors@1.0.0
    ├── utils-merge@1.0.0
    ├── cookie-signature@1.0.6
    ├── methods@1.1.1
    ├── fresh@0.2.4
    ├── cookie@0.1.2
    ├── escape-html@1.0.1
    ├── range-parser@1.0.2
    ├── content-type@1.0.1
    ├── finalhandler@0.3.3
    ├── vary@1.0.0
    ├── parseurl@1.3.0
    ├── content-disposition@0.5.0
    ├── path-to-regexp@0.1.3
    ├── depd@1.0.0
    ├── qs@2.3.3
    ├── on-finished@2.2.0 (ee-first@1.1.0)
    ├── etag@1.5.1 (crc@3.2.1)
    ├── debug@2.1.3 (ms@0.7.0)
    ├── proxy-addr@1.0.7 (forwarded@0.1.0, ipaddr.js@0.1.9)
    ├── send@0.12.1 (destroy@1.0.3, ms@0.7.0, mime@1.3.4)
    ├── serve-static@1.9.2 (send@0.12.2)
    ├── accepts@1.2.5 (negotiator@0.5.1, mime-types@2.0.10)
    └── type-is@1.6.1 (media-typer@0.3.0, mime-types@2.0.10)

    Vous pouvez utiliser la commande suivante pour vérifier tous les modules qui ont été installés globalement :

        $ npm ls -g

C-  Utilisation de package.json

    package.jsonest présent dans le répertoire racine de toute application/module Node et est utilisé pour définir les propriétés d'un package. Ouvrons package.jsonà partir du package express présent dans node_modules/express/

        (Voir fichier dans application node)

    C-1 : Les attributs de Package.json démystifiés

    *   nom − le nom du package
    *   version − la version du paquet
    *   description − la description du paquet
    *   page d'accueil − la page d'accueil du package
    *   auteur − l'auteur du paquet
    *   contributeurs − le nom des contributeurs au package
    *   dependencies − la liste des dépendances. NPM installe
        automatiquement toutes les dépendances mentionnées ici dans le dossier du package node_module.
    *   repository − le type de référentiel et l’URL du package.
    *   main − le point d’entrée du package.
    *   mots-clés − mots-clés.

    C-2 : Desinstallation d'un module 

    Utilisez la commande suivante pour désinstaller un module Node.js.

        $ npm uninstall express

    Une fois que NPM a désinstallé le package, vous pouvez le vérifier en regardant le contenu du répertoire /node_modules/ ou en tapant la commande suivante :

        $ npm ls

    C-3 : Mise à jour d'un module

    Mettez à jour package.json et modifiez la version de la dépendance à mettre à jour et exécutez la commande suivante.

        $ npm update express

    C-4 : Recharcher un module 

    Rechercher un nom de package à l'aide de NPM.

        $ npm search express

D-  Créer un module
    
    La création d'un module nécessite la génération de package.json. Générons package.json en utilisant npm init, ce qui générera le squelette de base de package.json.

        $ npm init
        This utility will walk you through the creation of a package.json file.
        It only covers the most common items, and tries to guess sane defaults.

        See 'npm help json' for definitive documentation on these fields
        and exactly what they do.

        Use 'npm install <pkg> --save' afterwards to install a package and
        save it as a dependency in the package.json file.

        Press ^C at any time to quit.
        name: (webmaster)

    Vous devrez fournir toutes les informations requises sur votre module. Vous pouvez vous aider du fichier package.json mentionné ci-dessus pour comprendre la signification des différentes informations demandées. Une fois le package.json généré, utilisez la commande suivante pour vous inscrire sur le site du référentiel NPM en utilisant une adresse e-mail valide.

        $ npm adduser
            Username: randomname
            Password:
            Email: (this IS public) randomname@gmail.com
        
    Il est temps de publier votre module.

        $ npm publish

    Si tout va bien avec votre module, il sera alors publié dans le référentiel et sera accessible à l'installation à l'aide de NPM comme n'importe quel autre module Node.js.