Chapitre : BOUCLE D'EVENEMENT

A-  NodeJS - Boucle d'évenements

    Node.js est une application monothread , mais elle peut prendre en charge la concurrence via le concept d' événement et de rappels . Chaque API Node.js est asynchrone et étant monothread, elles utilisent des appels de fonction asynchrones pour maintenir la concurrence. Node utilise des modèles d'observateur. Le thread Node conserve une boucle d'événements et chaque fois qu'une tâche est terminée, il déclenche l'événement correspondant qui signale à la fonction d'écoute d'événements de s'exécuter.

B-  Programmation pilotée par événements

    Node.js utilise beaucoup les événements et c'est aussi l'une des raisons pour lesquelles Node.js est assez rapide par rapport à d'autres technologies similaires. Dès que Node démarre son serveur, il initialise simplement ses variables, déclare des fonctions et attend simplement que l'événement se produise.

    Dans une application pilotée par événements, il existe généralement une boucle principale qui écoute les événements, puis déclenche une fonction de rappel lorsqu'un de ces événements est détecté.

        https://i.imgur.com/UvrDlCD.jpg

B-  Boucle d'événement

        https://i.imgur.com/UvrDlCD.jpg

    Bien que les événements ressemblent beaucoup aux rappels, la différence réside dans le fait que les fonctions de rappel sont appelées lorsqu'une fonction asynchrone renvoie son résultat, tandis que la gestion des événements fonctionne selon le modèle d'observateur. Les fonctions qui écoutent les événements agissent comme des observateurs. Chaque fois qu'un événement est déclenché, sa fonction d'écoute commence à s'exécuter. Node.js dispose de plusieurs événements intégrés disponibles via le module events et les classes EventEmitter qui sont utilisés pour lier les événements et les écouteurs d'événements comme suit :

        // Import events module
        var events = require('events');

        // Create an eventEmitter object
        var eventEmitter = new events.EventEmitter();

    Voici la syntaxe pour lier un gestionnaire d’événements à un autre événement :

        // Bind event and event  handler as follows
        eventEmitter.on('eventName', eventHandler);

    Nous pouvons déclencher un événement par programmation comme suit :

        // Fire an event 
        eventEmitter.emit('eventName');

        Exemple :

        Créez un fichier .js nommé main.js avec le code suivant :

            // Import events module
            var events = require('events');

            // Create an eventEmitter object
            var eventEmitter = new events.EventEmitter();

            // Create an event handler as follows
            var connectHandler = function connected() {
            console.log('connection succesful.');
            
            // Fire the data_received event 
            eventEmitter.emit('data_received');
            }

            // Bind the connection event with the handler
            eventEmitter.on('connection', connectHandler);
            
            // Bind the data_received event with the anonymous function
            eventEmitter.on('data_received', function() {
            console.log('data received succesfully.');
            });

            // Fire the connection event 
            eventEmitter.emit('connection');

            console.log("Program Ended.");

        Essayons maintenant d’exécuter le programme ci-dessus et de vérifier sa sortie :

            $ node main.js
            
            Cela devrait produire le résultat suivant :

            connection successful.
            data received successfully.
            Program Ended.

    
E-  Comment fonctionnent les applications Node ?

    Dans Node Application, toute fonction asynchrone accepte un rappel comme dernier paramètre et une fonction de rappel accepte une erreur comme premier paramètre. Reprenons l'exemple précédent. Créez un fichier texte nommé input.txt avec le contenu suivant :

        Dummy Text Just for Testing !!!!

    Créez un fichier .js nommé main.js contenant le code suivant :

    var fs = require("fs");

    fs.readFile('input.txt', function (err, data) {
    if (err) {
        console.log(err.stack);
        return;
    }
    console.log(data.toString());
    });
    console.log("Program Ended");

    Ici, fs.readFile() est une fonction asynchrone dont le but est de lire un fichier. Si une erreur se produit pendant l'opération de lecture, l' objet err contiendra l'erreur correspondante, ou bien data contiendra le contenu du fichier. readFile transmet (err) et data à la fonction de rappel une fois l'opération de lecture terminée, qui imprime finalement ce contenu :

        Program Ended
        Dummy Text Just for Testing !!!!

