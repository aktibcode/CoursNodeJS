Chapitre : EMETTEUR D'EVENEMENT

A-  Classe EventEmitter

    De nombreux objets dans un nœud émettent des événements. Par exemple, un net.Server émet un événement à chaque fois qu'un homologue s'y connecte. Un fs.readStream émet un événement lorsque le fichier est ouvert. Tous les objets qui émettent des événements sont les instances de events.EventEmitter.

    Comme nous l'avons vu dans la section précédente, la classe EventEmitter se trouve dans le module events. Elle est accessible via le code suivant :

        // Import events module
        var events = require('events');

        // Create an eventEmitter object
        var eventEmitter = new events.EventEmitter();

    Lorsqu'une instance EventEmitter rencontre une erreur, elle émet un événement « error ». Lorsqu'un nouvel écouteur est ajouté, l'événement « newListener » est déclenché et lorsqu'un écouteur est supprimé, l'événement « removeListener » est déclenché.

    EventEmitter fournit plusieurs propriétés telles que on et emit. La propriété on est utilisée pour lier une fonction à l'événement et emit est utilisée pour déclencher un événement.

B-  Méthodes

    *   addListener(event, listener) : Ajoute un écouteur à la fin du tableau d'écouteurs pour l'événement spécifié. Aucune vérification n'est effectuée pour voir si l'écouteur a déjà été ajouté. Plusieurs appels transmettant la même combinaison d'événement et d'écouteur entraîneront l'ajout de l'écouteur plusieurs fois. Renvoie l'émetteur, les appels peuvent donc être chaînés.

    *   on(event, listener) : Ajoute un écouteur à la fin du tableau d'écouteurs pour l'événement spécifié. Aucune vérification n'est effectuée pour voir si l'écouteur a déjà été ajouté. Plusieurs appels transmettant la même combinaison d'événement et d'écouteur entraîneront l'ajout de l'écouteur plusieurs fois. Renvoie l'émetteur, les appels peuvent donc être chaînés.

    *   once(event, listener) : Ajoute un écouteur ponctuel à l'événement. Cet écouteur n'est invoqué que la prochaine fois qu'un événement est déclenché, après quoi il est supprimé. Renvoie l'émetteur, afin que les appels puissent être chaînés.

    *   removeListener(event, listener) : supprime un écouteur du tableau d'écouteurs pour l'événement spécifié. Attention − Cela modifie les indices de tableau dans le tableau d'écouteurs derrière l'écouteur. removeListener supprimera, dans la plupart des cas, une instance d'un écouteur du tableau d'écouteurs. Si un seul écouteur a été ajouté plusieurs fois au tableau d'écouteurs pour l'événement spécifié, removeListener doit être appelé plusieurs fois pour supprimer chaque instance. Renvoie l'émetteur, les appels peuvent donc être chaînés.

    *   removeAllListeners([event]) : supprime tous les écouteurs, ou ceux de l'événement spécifié. Ce n'est pas une bonne idée de supprimer les écouteurs qui ont été ajoutés ailleurs dans le code, en particulier lorsqu'ils se trouvent sur un émetteur que vous n'avez pas créé (par exemple, des sockets ou des flux de fichiers). Renvoie l'émetteur, afin que les appels puissent être chaînés.

    *   setMaxListeners(n) : Par défaut, EventEmitters affichera un avertissement si plus de 10 écouteurs sont ajoutés pour un événement particulier. Il s'agit d'un état par défaut utile qui permet de trouver des fuites de mémoire. Évidemment, tous les émetteurs ne doivent pas être limités à 10. Cette fonction permet d'augmenter ce nombre. Réglez-le sur zéro pour un nombre illimité.

    *   listeners(event) : renvoie un tableau d'écouteurs pour l'événement spécifié.

    *   emit(event, [arg1], [arg2], [...]) : exécute chacun des écouteurs dans l'ordre avec les arguments fournis. Renvoie true si l'événement avait des écouteurs, false sinon.

C-  Méthodes de classe

    listenerCount(emitter, event) : Renvoie le nombre d'écouteurs pour un événement donné.

        *   Exemple : créez un fichier nommé listenerCount.js enregistré sur votre machine,

        //import event module
    var events = require('events');
        // Create an eventEmitter object
    var eventEmitter = new events.EventEmitter();
    eventEmitter.on('connection',function(){
        console.log("hello connection")
    });
        // count the number of listener to this event
    eventListeners = require('events').EventEmitter.listenerCount(eventEmitter,'connection');
    console.log(eventListeners + " Listner(s) listening to connection event");

    Exécutez ce morceau de code en exécutant la commande suivante :

        $ node listenerCount.js

            *   Sortir:
            
            1  Listner(s) listening to connection event

D-  Evénements

    *   newLister
        *   event − Chaîne : le nom de l'événement
        *   listener − Fonction : fonction du gestionnaire d'événements.
            Cet événement est émis à chaque fois qu'un écouteur est ajouté. Lorsque cet événement est déclenché, l'écouteur n'a peut-être pas encore été ajouté au tableau d'écouteurs pour l'événement.

    *   removeListener

        *   event − Chaîne : le nom de l’événement.
        *   listener − Fonction : fonction du gestionnaire d'événements.
            Cet événement est émis à chaque fois que quelqu'un supprime un écouteur. Lorsque cet événement est déclenché, l'écouteur n'a peut-être pas encore été supprimé du tableau d'écouteurs pour l'événement.

    Exemple 

        Créez un fichier .js nommé main.js avec le code Node.js suivant

        var events = require('events');
        var eventEmitter = new events.EventEmitter();

        // listener #1
        var listner1 = function listner1() {
            console.log('listner1 executed.');
        }

        // listener #2
        var listner2 = function listner2() {
            console.log('listner2 executed.');
        }

        // Bind the connection event with the listner1 function
        eventEmitter.addListener('connection', listner1);

        // Bind the connection event with the listner2 function
        eventEmitter.on('connection', listner2);

        var eventListeners = require('events').EventEmitter.listenerCount
        (eventEmitter,'connection');
        console.log(eventListeners + " Listner(s) listening to connection event");

        // Fire the connection event 
        eventEmitter.emit('connection');

        // Remove the binding of listner1 function
        eventEmitter.removeListener('connection', listner1);
        console.log("Listner1 will not listen now.");

        // Fire the connection event 
        eventEmitter.emit('connection');

        eventListeners = require('events').EventEmitter.listenerCount(eventEmitter,'connection');
        console.log(eventListeners + " Listner(s) listening to connection event");

        console.log("Program Ended.");

    Exécutez maintenant le main.js pour voir le résultat.

            $ node main.js
        
        Vérifier la sortie

        2 Listner(s) listening to connection event
        listner1 executed.
        listner2 executed.
        Listner1 will not listen now.
        listner2 executed.
        1 Listner(s) listening to connection event
        Program Ended.


