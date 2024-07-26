Chapitre : Objets Globaux

A-  _filename (Nom de fichier)

    Les objets globaux de Node.js sont de nature globale et sont disponibles dans tous les modules. Nous n'avons pas besoin d'inclure ces objets dans notre application, mais nous pouvons les utiliser directement. Ces objets sont des modules, des fonctions, des chaînes et des objets eux-mêmes. Nous vous en dirons plus dans les prochaines diapositives.

    Le __filenamereprésente le nom de fichier du code en cours d'exécution. Il s'agit du chemin absolu résolu du fichier de code. Pour un programme principal, il ne s'agit pas nécessairement du même nom de fichier que celui utilisé dans la ligne de commande. La valeur à l'intérieur d'un module est le chemin d'accès au fichier de ce module.

    Exemple
    
        Créez un fichier .js nommé main.js avec le code suivant :

        // Let's try to print the value of __filename
        
        console.log( __filename );

    Exécutez maintenant le main.js pour voir le résultat :

        $ node main.js
    
    En fonction de l'emplacement de votre programme, il imprimera le nom du fichier principal comme suit :

        /web/com/1427091028_21099/main.js

B-  __dirname (repertoire)

    Le __dirname représente le nom du répertoire dans lequel réside le script en cours d'exécution.

    Exemple
    
        Créez un fichier .js nommé main.js avec le code suivant :

        // Let's try to print the value of __dirname

        console.log( __dirname );
    
    Exécutez maintenant le main.js pour voir le résultat :

        $ node main.js
    
    En fonction de l'emplacement de votre programme, il imprimera les noms des répertoires actuels comme suit :

        /web/com/1427091028_21099

C-  setTimeout(cb, ms)

    La fonction globale setTimeout(cb, ms) est utilisée pour exécuter le rappel (cb) après au moins ms millisecondes . Le délai réel dépend de facteurs externes tels que la granularité du minuteur du système d'exploitation et la charge du système. Un minuteur ne peut pas s'étendre sur plus de 24,8 jours.

    Exemple

        Créez un fichier .js nommé main.js avec le code suivant :

            function printHello() {
                
                console.log( "Hello, World!");
            
            }

            // Now call above function after 2 seconds
            setTimeout(printHello, 2000);

        Exécutez maintenant le main.js pour voir le résultat :

            $ node main.js
        
        Vérifiez que la sortie est imprimée comme après un petit délai :

        Hello, World!

D-  clearTimeout(t)

    La fonction globale clearTimeout(t) permet d'arrêter un minuteur précédemment créé avec setTimeout() . Ici, t est le minuteur renvoyé par la fonction setTimeout() .

    Exemple
    
        Créez un fichier .js nommé main.js avec le code suivant :

        function printHello() {

            console.log( "Hello, World!");
        
        }

            // Now call above function after 2 seconds
        
        var t = setTimeout(printHello, 2000);

            // Now clear the timer
        
        clearTimeout(t);

    Exécutez maintenant le main.js pour voir le résultat :

    $ node main.js
    
    Vérifiez la sortie où vous ne trouverez rien d'imprimé.


E-  setInterval(cb, ms)

    La fonction globale setInterval(cb, ms) est utilisée pour exécuter un rappel cb de manière répétée après au moins quelques millisecondes. Le délai réel dépend de facteurs externes tels que la granularité du minuteur du système d'exploitation et la charge du système. Un minuteur ne peut pas s'étendre sur plus de 24,8 jours.

    Cette fonction renvoie une valeur opaque qui représente le minuteur qui peut être utilisé pour effacer le minuteur à l'aide de la fonction clearInterval(t) .

    Exemple

        Créez un fichier .js nommé main.js avec le code suivant :

        function printHello() {
            
            console.log( "Hello, World!");
        
        }

        // Now call above function after 2 seconds

        setInterval(printHello, 2000);

    Exécutez maintenant le main.js pour voir le résultat :

        $ node main.js

    Le programme ci-dessus exécutera printHello() toutes les 2 secondes. En raison d'une limitation du système.
