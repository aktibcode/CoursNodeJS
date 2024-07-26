Chapitre : MODULE WEB 

A-  Qu'est-ce qu'un serveur Web ?

    Un serveur Web est une application logicielle qui gère les requêtes HTTP envoyées par le client HTTP, comme les navigateurs Web, et renvoie des pages Web en réponse aux clients. Les serveurs Web fournissent généralement des documents HTML accompagnés d'images, de feuilles de style et de scripts.

    La plupart des serveurs Web prennent en charge les scripts côté serveur. Ils utilisent des langages de script et redirigent la tâche vers un serveur d'application qui récupère les données d'une base de données et exécute une logique complexe. Enfin, un résultat est envoyé au client HTTP via le serveur Web.

B-  Architecture des applications Web

    Une application Web est généralement divisée en quatre couches :

        https://i.imgur.com/GXhlHeD.png

        *   Client : Cette couche est constituée de navigateurs Web, de navigateurs mobiles ou d'applications qui peuvent effectuer des requêtes HTTP vers le serveur Web.
        
        *   Serveur : Cette couche possède le serveur web qui peut intercepter les requêtes faites par les clients et leur transmettre la réponse.
       
        *   Métier : Cette couche contient le serveur d'application qui est utilisé par le serveur Web pour effectuer les traitements requis. Cette couche interagit avec la couche de données via la base de données ou certains programmes externes.
        
        *   Données : Cette couche contient les bases de données ou toute autre source de données.

C-  Créer un serveur Web à l'aide de Node
    
    Node.js fournit un module HTTP qui peut être utilisé pour créer un client HTTP d'un serveur. Voici la structure minimale du serveur HTTP qui écoute le port 8081.

        Créez un fichier js nommé server.js :

        Fichier : server.js

            var http = require('http');
           
            var fs = require('fs');
            
            var url = require('url');

                // Create a server

            http.createServer( function (request, response) {  
                
                // Parse the request containing file name
                
                var pathname = url.parse(request.url).pathname;
                
                // Print the name of the file for which request is made.
                
                console.log("Request for " + pathname + " received.");
                
                // Read the requested file content from file system
                
                fs.readFile(pathname.substr(1), function (err, data) {
                    
                    if (err) {
                        
                        console.log(err);
                        
                        // HTTP Status: 404 : NOT FOUND
                        // Content Type: text/plain
                        
                        response.writeHead(404, {'Content-Type': 'text/html'});
                    
                    } else {	
                        
                        //Page found	  
                        // HTTP Status: 200 : OK
                        // Content Type: text/plain
                        
                        response.writeHead(200, {'Content-Type': 'text/html'});	
                        
                        // Write the content of the file to response body
                        
                        response.write(data.toString());		
                    
                    }
                    
                    // Send the response body 
                    
                    response.end();
                });   
            }).listen(8081);

                // Console will print the message
                console.log('Server running at http://127.0.0.1:8081/');

        Ensuite, créons le fichier HTML suivant nommé index.html dans le même répertoire où vous avez créé server.js.

            Fichier: index.html

            <html>
                <head>
                    <title>Sample Page</title>
                </head>
                
                <body>
                    Hello World!
                </body>
            </html>

        Exécutons maintenant le server.js pour voir le résultat :

            $ node server.js
        
        Vérifier la sortie

            Server running at http://127.0.0.1:8081/

D-  Faire une requête au serveur Node.js.

    Ouvrez http://127.0.0.1:8081/index.htm dans n'importe quel navigateur et vous devriez voir notre « Hello World » affiché sur la page.

        https://i.imgur.com/C4F9Ceh.jpg

        Vérifiez la sortie côté serveur :

            Server running at http://127.0.0.1:8081/
            
            Request for /index.htm received.


E-  Créer un client Web à l'aide de Node

    Un client Web peut être créé à l'aide du module HTTP . Voyons l'exemple suivant.

        Créez un fichier .js nommé client.js :

        Fichier : client.js

        var http = require('http');

        // Options to be used by request 
        
        var options = {
            host: 'localhost',
            port: '8081',
            path: '/index.html'  
        };

        // Callback function is used to deal with a response
        
        var callback = function(response) {
        
            // Continuously update stream with data
            
            var body = '';
                
            response.on('data', function(data) {
                    
                    body += data;
            
            });
            
            response.on('end', function() {
                
                // Data received completely.
                
                console.log(body);
            
            });
        }
        
        // Make a request to the server
        
        var req = http.request(options, callback);
        
        req.end();

    Exécutez maintenant le client.js à partir d’un autre terminal de commande que server.js pour voir le résultat :

        $ node client.js
    
    Vérifiez la sortie :

        <html>
            <head>
                <title>Sample Page</title>
            </head>
            
            <body>
                Hello World!
            </body>
        </html>
    
    Vérifiez la sortie côté serveur :

        Server running at http://127.0.0.1:8081/
        Request for /index.htm received.
