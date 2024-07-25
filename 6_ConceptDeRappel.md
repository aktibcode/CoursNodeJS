Chapitre : CONCEPT DE RAPPELS

A-  Qu'est ce que le rappel

    Le rappel est l'équivalent asynchrone d'une fonction. Une fonction de rappel est appelée à la fin d'une tâche donnée. Node fait un usage intensif des rappels. Toutes les API Node sont écrites de manière à prendre en charge les rappels.

    Par exemple, une fonction de lecture de fichier peut commencer à lire des fichiers et renvoyer immédiatement le contrôle à l'environnement d'exécution afin que l'instruction suivante puisse être exécutée. Une fois l'E/S du fichier terminée, elle appellera la fonction de rappel tout en passant à la fonction de rappel, le contenu du fichier en tant que paramètre. Il n'y a donc pas de blocage ni d'attente pour l'E/S du fichier. Cela rend Node.js hautement évolutif car il peut traiter un grand nombre de requêtes sans attendre qu'une fonction renvoie des résultats.

    https://youtu.be/3DW0T2W3P7Y

B-  Exemple de code de blocage

    Créez un fichier texte nommé input.txt avec le contenu suivant :

        Random Text Just For Testing!!!
    
    Créez un fichier .js nommé main.js avec le code suivant :

        var fs = require("fs");
        // fs is the file system module we will see it later
        var data = fs.readFileSync('input.txt');

        console.log(data.toString());
        console.log("Program Ended");

    Exécutez maintenant le main.js pour voir le résultat :

        $ node main.js

    Vérifiez la sortie :

        Random Text Just For Testing!!!
        Program Ended

C-  Exemple de code non bloquant

    Créez un fichier texte nommé input.txt avec le contenu suivant :

        Random Text Just For Testing!!!

    Mettez à jour main.js pour avoir le code suivant :

        var fs = require("fs");

        fs.readFile('input.txt', function (err, data) {
            //this is the callBack function
            if (err) return console.error(err);
            console.log(data.toString());
        });

        console.log("Program Ended");

    Exécutez maintenant le main.js pour voir le résultat :

        $ node main.js

    Vérifiez la sortie :

        Program Ended
        Random Text Just For Testing!!!

D-  Blocage vs non-Blocage

    Ces deux exemples expliquent le concept d'appels bloquants et non bloquants.

        *   Le premier exemple montre que le programme bloque l'appel jusqu'à ce qu'il lise le fichier et seulement ensuite il procède à la fin du programme.
        *   Le deuxième exemple montre que le programme n'attend pas la lecture du fichier et procède à l'impression de "Programme terminé" et en même temps, le programme, sans blocage, continue la lecture du fichier.
    Ainsi, un programme bloquant est exécuté de manière séquentielle. D'un point de vue de la programmation, il est plus facile d'implémenter la logique, mais les programmes non bloquants ne s'exécutent pas de manière séquentielle. Dans le cas où un programme doit utiliser des données à traiter, celles-ci doivent être conservées dans le même bloc pour en faire une exécution séquentielle.

    https://i.imgur.com/zzQtJV3.png

    