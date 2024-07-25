Chapitre :  TERMINAL REPL 


A-  Démarrage de REPL 

    REPL signifie Read Eval Print Loop et représente un environnement informatique comme une console Windows ou un shell Unix/Linux où une commande est entrée et le système répond avec une sortie en mode interactif. Node.js ou Node est fourni avec un environnement REPL. Il effectue les tâches suivantes :

        *   Lire – Lit l’entrée de l’utilisateur, analyse l’entrée dans la structure de données JavaScript et la stocke en mémoire.

        *   Eval − Prend et évalue la structure de données.

        *   Imprimer – Imprime le résultat.

        *   Boucle – Boucle la commande ci-dessus jusqu’à ce que l’utilisateur appuie deux fois sur ctrl-c .

    La fonctionnalité REPL de Node est très utile pour expérimenter les codes Node.js et déboguer les codes JavaScript.
    REPL peut être démarré en exécutant simplement node sur le shell/la console sans aucun argument comme suit.

        $ node

    Vous verrez l’invite de commande REPL > où vous pouvez taper n’importe quelle commande Node.js.

        $ node
        >

    A-1 : Expression simple

        Essayons quelques mathématiques simples avec l'invite de commande REPL de Node.js :

        $ node
        > 1 + 3
        4
        > 1 + ( 2 * 3 ) - 4
        3
        >

    A-2 : Utiliser des variables 

        Vous pouvez utiliser des variables pour stocker des valeurs et les imprimer ultérieurement comme n'importe quel script conventionnel. Si le mot-clé var n'est pas utilisé, la valeur est stockée dans la variable et imprimée. En revanche, si le mot-clé var est utilisé, la valeur est stockée mais pas imprimée. Vous pouvez imprimer des variables à l'aide de console.log() .

        $ node
        > x = 10
        10
        > var y = 10
        undefined
        > x + y
        20
        > console.log("Hello World")
        Hello World
        undefined

    A-3 Expression multiligne 

        Node REPL prend en charge les expressions multilignes similaires à JavaScript. Voyons la boucle do-while suivante en action.

        $ node
        > var x = 0
        undefined
        > do {
        ... x++;
        ... console.log("x: " + x);
        ... } 
        while ( x < 5 );
        x: 1
        x: 2
        x: 3
        x: 4
        x: 5
        undefined
        >

        .. s'affiche automatiquement lorsque vous appuyez sur Entrée après la parenthèse ouvrante. Node vérifie automatiquement la continuité des expressions.

    A-4 Varable de soulignement 

        Vous pouvez utiliser le trait de soulignement (_) pour obtenir le dernier résultat

        $ node
        > var x = 10
        undefined
        > var y = 20
        undefined
        > x + y
        30
        > var sum = _
        undefined
        > console.log(sum)
        30
        undefined
        >

B-  Commandes REPL

    *   ctrl + c − termine la commande en cours.

    *   ctrl + c deux fois − termine le nœud REPL.
    
    *   ctrl + d − termine le nœud REPL.
    
    *   Touches Haut/Bas – voir l’historique des commandes et modifier les commandes précédentes.
    
    *   Tab Touches − répertorie toutes les commandes actuelles.
    
    *   .help − répertorie toutes les commandes.
    
    *   .break − quitte l’expression multiligne.
    
    *   .clear − quitte l’expression multiligne.
    
    *   .save filename − enregistre la session Node REPL actuelle dans un fichier.
    
    *   .load filename − charge le contenu du fichier à partir de la session Node REPL actuelle.

C-  Arrete REPL 

    Comme mentionné ci-dessus, vous devrez utiliser ctrl-c deux fois pour sortir de Node.js REPL.

        $ node
        >
        (^C again to quit)
        >