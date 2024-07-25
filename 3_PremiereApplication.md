Chapitre : PREMIERE APPLICATION


A-  Première Application

    Avant de créer une véritable application « Hello, World ! » à l'aide de Node.js, examinons les composants d'une application Node.js. Une application Node.js se compose des trois composants importants suivants :

    *   Importer les modules requis : Nous utilisons la directive require pour charger les modules Node.js.
    *   Créer un serveur : un serveur qui écoutera les requêtes du client, similaire au serveur HTTP Apache.
    *   Lire la requête et renvoyer la réponse : Le serveur créé à une étape précédente lira la requête HTTP effectuée par le client qui peut être un navigateur ou une console, puis renverra la réponse.

B-  Création d'une application Node.js

    Étape 1 – Importer le module requis
    Nous utilisons la requiredirective pour charger le module HTTP et stocker l'instance HTTP renvoyée dans une variable HTTP comme suit :

        var http = require("http");

    Étape 2 – Créer un serveur

    Nous utilisons l'instance HTTP créée et http.createServer()la méthode d'appel pour créer une instance de serveur, puis nous la lions au port 8081 à l'aide de la listenméthode associée à l'instance de serveur. Nous lui passons une fonction avec les paramètres requestet response.
    Écrivez l'exemple d'implémentation pour toujours renvoyer « Hello World ».

    http.createServer(function (request, response) {
        // Send the HTTP header 
        // HTTP Status: 200 : OK
        // Content Type: text/plain
        response.writeHead(200, {'Content-Type': 'text/plain'});
        
        // Send the response body as "Hello World"
        response.end('Hello World\n');
    }).listen(8081);
        
        // Console will print the message
        console.log('Server running at http://127.0.0.1:8081/');

    Le code ci-dessus suffit à créer un serveur HTTP qui écoute, c'est-à-dire qui attend une requête sur le port 8081 sur la machine locale.

    Étape 3 – Demande de test et réponse.

        Rassemblons les étapes 1 et 2 dans un fichier appelé main.js et démarrons notre serveur HTTP comme indiqué ci-dessous :

        var http = require("http");

        http.createServer(function (request, response) {
            // Send the HTTP header 
            // HTTP Status: 200 : OK
            // Content Type: text/plain
        response.writeHead(200, {'Content-Type': 'text/plain'});
        
            // Send the response body as "Hello World"
        response.end('Hello World\n');
        }).listen(8081);

            // Console will print the message
        console.log('Server running at http://127.0.0.1:8081/');

    Exécutez maintenant le fichier main.js pour démarrer le serveur comme suit :

        $ node main.js

    Vérifiez la sortie. Le serveur a démarré.

        Server running at http://127.0.0.1:8081/

    Faire une requête au serveur Node.js
        
        Ouvrez http://127.0.0.1:8081/ dans n’importe quel navigateur et observez le résultat suivant.

        https://i.imgur.com/7xsp470.jpg

