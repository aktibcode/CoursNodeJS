Chapitre : SYSTEME DE FICHIER

A-  Synchrone vs Asynchrone

    Node implémente les E/S de fichiers à l'aide de simples wrappers autour des fonctions POSIX standard. Le module Node File System (fs) peut être importé à l'aide de la syntaxe suivante :

        var fs = require("fs")

    Chaque méthode du module FS possède des formes synchrones et asynchrones. Les méthodes asynchrones prennent le dernier paramètre comme rappel de la fonction de complétion et le premier paramètre de la fonction de rappel comme erreur. Il est préférable d'utiliser une méthode asynchrone plutôt qu'une méthode synchrone, car la première ne bloque jamais un programme pendant son exécution, alors que la seconde le fait.

    Exemple

        Créez un fichier texte nommé input.txt avec le contenu suivant :

        Dummy Text For Testing !!!!

    Créons un fichier .js nommé main.js avec le code suivant :

        var fs = require("fs");

        // Asynchronous read
        fs.readFile('input.txt', function (err, data) {
        if (err) {
            return console.error(err);
        }
        console.log("Asynchronous read: " + data.toString());
        });
        
        // Synchronous read
        var data = fs.readFileSync('input.txt');
        console.log("Synchronous read: " + data.toString());

        console.log("Program Ended");

    Exécutez maintenant le main.js pour voir le résultat

        $ node main.js

    Vérifiez la sortie :

        Synchronous read: Dummy Text For Testing !!!!

        Program Ended
        Asynchronous read: Dummy Text For Testing !!!!

    Jetons un œil à un ensemble de bons exemples sur les principales méthodes d’E/S de fichiers :



B-  Ouvrir un fichier

    Syntaxe

    Voici la syntaxe de la méthode pour ouvrir un fichier en mode asynchrone :

    fs.open(path, flags[, mode], callback)

    Paramètres

    Voici la description des paramètres utilisés :

        *   chemin – Il s’agit de la chaîne contenant le nom du fichier et le chemin.

        *   flags − Les flags indiquent le comportement du fichier à ouvrir. Toutes les valeurs possibles ont été mentionnées ci-dessous.

        *   mode − Définit le mode du fichier (autorisation et bits collants), mais uniquement si le fichier a été créé. La valeur par défaut est 0666, accessible en lecture et en écriture.

        *   callback − Il s’agit de la fonction de rappel qui reçoit deux arguments (err, fd).

    Flags

        r : ouvre le fichier en lecture. Une exception se produit si le fichier n'existe pas.

        r+ : ouvre le fichier en lecture et en écriture. Une exception se produit si le fichier n'existe pas.

        rs : Ouvre le fichier en lecture en mode synchrone.

        rs+ : ouvre le fichier en lecture et en écriture, en demandant au système d'exploitation de l'ouvrir de manière synchrone. Consultez les notes sur « rs » pour savoir comment utiliser cette fonction avec précaution.

        w : Ouvre le fichier en écriture. Le fichier est créé (s'il n'existe pas) ou tronqué (s'il existe).

        wx : Comme 'w' mais échoue si le chemin existe.

        w+ : Ouvre le fichier en lecture et en écriture. Le fichier est créé (s'il n'existe pas) ou tronqué (s'il existe).

        wx+ : comme 'w+' mais échoue si le chemin existe.

        a : Ouvre le fichier pour l'ajouter. Le fichier est créé s'il n'existe pas.

        ax : Comme 'a' mais échoue si le chemin existe.

        a+ : Ouvre le fichier pour lecture et ajout. Le fichier est créé s'il n'existe pas.

        ax+ : Comme 'a+' mais échoue si le chemin existe.

    Exemple

        Créons un fichier .js nommé main.js qui contient le code suivant pour ouvrir un fichier input.txt pour la lecture et l'écriture :

        var fs = require("fs");

        // Asynchronous - Opening File

        console.log("Going to open file!");

        fs.open('input.txt', 'r+', function(err, fd) {

            if (err) {
                return console.error(err);
            }

            console.log("File opened successfully!"); 

        });

        Exécutez maintenant le main.js pour voir le résultat :

            $ node main.js

        Vérifiez la sortie :

            Going to open file!
            File opened successfully!



C-  Obtenir les informations d'un fichier

    Syntaxe

    Voici l'une des syntaxes des méthodes permettant d'obtenir les informations du fichier :

        fs.stat(path, callback)

    Paramètres

    Voici la description des paramètres utilisés :

        chemin – Il s’agit de la chaîne contenant le nom du fichier et le chemin.

        callback − Il s'agit de la fonction de rappel qui obtient deux arguments (err, stats) où stats est un objet de type fs.Stats qui est imprimé ci-dessous dans l'exemple.

    Outre les attributs importants qui sont imprimés ci-dessous dans l'exemple, il existe plusieurs méthodes utiles disponibles dans la classe fs.Stats qui peuvent être utilisées pour vérifier le type de fichier. Ces méthodes sont données dans la liste suivante :

        *   stats.isFile() : Renvoie true si le type de fichier est un fichier simple.

        *   stats.isDirectory() : Renvoie vrai si le type de fichier d'un répertoire.

        *   stats.isBlockDevice() : Renvoie true si le type de fichier est un périphérique de bloc.

        *   stats.isCharacterDevice() : Renvoie true si le type de fichier est un périphérique de caractères.

        *   stats.isSymbolicLink() : Renvoie true si le type de fichier d'un lien symbolique.

        *   stats.isFIFO() : Renvoie vrai si le type de fichier est un FIFO.

        *   stats.isSocket() : Renvoie true si le type de fichier est asocket.

    Exemple

    Créons un fichier js nommé main.js avec le code suivant

        var fs = require("fs");

        console.log("Going to get file info!");

        fs.stat('input.txt', function (err, stats) {

            if (err) {
                return console.error(err);
            }

        console.log(stats);

        console.log("Got file info successfully!");
        
        // Check file type

            console.log("isFile ? " + stats.isFile());

            console.log("isDirectory ? " + stats.isDirectory());    
        });

    Exécutez maintenant le main.js pour voir le résultat

        $ node main.js

    Vérifier la sortie

        Going to get file info!

        { 
            dev: 1792,
            mode: 33188,
            nlink: 1,
            uid: 48,
            gid: 48,
            rdev: 0,
            blksize: 4096,
            ino: 4318127,
            size: 97,
            blocks: 8,
            atime: Sun Mar 22 2015 13:40:00 GMT-0500 (CDT),
            mtime: Sun Mar 22 2015 13:40:57 GMT-0500 (CDT),
            ctime: Sun Mar 22 2015 13:40:57 GMT-0500 (CDT) 
        }
            Got file info successfully!

            isFile ? true
            isDirectory ? false


D-  Écriture d'un fichier
    
    Syntaxe

        Voici l'une des syntaxes des méthodes permettant d'écrire dans un fichier :

            fs.writeFile(filename, data[, options], callback)
    
    Cette méthode écrasera le fichier si celui-ci existe déjà. Si vous souhaitez écrire dans un fichier existant, vous devez utiliser une autre méthode disponible.

    Paramètres
    
        Voici la description des paramètres utilisés :

        *   chemin − Il s’agit de la chaîne contenant le nom du fichier, y compris le chemin.

        *   données − Il s’agit de la chaîne ou du tampon à écrire dans le fichier.

        *   options − Le troisième paramètre est un objet qui contiendra {encoding, mode, flag}. Par défaut, l'encodage est utf8, le mode est la valeur octale 0666 et le flag est 'w'

        *   callback − Il s'agit de la fonction de rappel qui reçoit un seul paramètre err qui renvoie une erreur en cas d'erreur d'écriture.

    Exemple

        Créons un fichier js nommé main.js contenant le code suivant :

            var fs = require("fs");

            console.log("Going to write into existing file");

            fs.writeFile('input.txt', 'Simply Easy Learning!', function(err) {

                if (err) {
                    return console.error(err);
                }
                
                console.log("Data written successfully!");

                console.log("Let's read newly written data");
                
                fs.readFile('input.txt', function (err, data) {

                    if (err) {
                        return console.error(err);
                    }

                    console.log("Asynchronous read: " + data.toString());
                });
            });

        Exécutez maintenant le main.js pour voir le résultat

            $ node main.js
        
        Vérifier la sortie

        Going to write into existing file
        Data written successfully!
        Let's read newly written data
        Asynchronous read: Simply Easy Learning!


E-  Lire un fichier

    Syntaxe

        Voici l'une des syntaxes des méthodes permettant de lire un fichier :

            fs.read(fd, buffer, offset, length, position, callback)
    
    Cette méthode utilisera un descripteur de fichier pour lire le fichier. Si vous souhaitez lire le fichier directement en utilisant le nom du fichier, vous devez utiliser une autre méthode disponible.

    Paramètres

        Voici la description des paramètres utilisés :

        *   fd − Il s’agit du descripteur de fichier renvoyé par fs.open().

        *   tampon − Il s’agit du tampon dans lequel les données seront écrites.

        *   offset − Il s’agit du décalage dans le tampon à partir duquel l’écriture doit commencer.

        *   longueur − Il s’agit d’un entier spécifiant le nombre d’octets à lire.

        *   position − Il s'agit d'un entier spécifiant où commencer la lecture à l'intérieur du fichier. Si une position est nulle, les données seront lues à partir de la position actuelle du fichier.

        *   callback − Il s'agit de la fonction de rappel qui récupère les trois arguments (err, bytesRead, buffer)

    Exemple

    Créons un fichier .js nommé main.js avec le code suivant :

        var fs = require("fs");
        var buf = new Buffer.alloc(1024);

        console.log("Going to open an existing file");

        fs.open('input.txt', 'r+', function(err, fd) {

            if (err) {
                return console.error(err);
            }

            console.log("File opened successfully!");

            console.log("Going to read the file");
            
            fs.read(fd, buf, 0, buf.length, 0, function(err, bytes){

                if (err){
                    console.log(err);
                }

                console.log(bytes + " bytes read");

                // Print only read bytes to avoid junk.

                if(bytes > 0){
                    console.log(buf.slice(0, bytes).toString());
                }

            });
        });

        Exécutez maintenant le main.js pour voir le résultat :

            $ node main.js
        
        Vérifier la sortie

            Going to open an existing file
            File opened successfully!
            Going to read the file
            67 bytes read
            Dummy Text For Testing!!!!!


F-  Fermeture d'un dossier

    Syntaxe
        
        Voici la syntaxe pour fermer un fichier ouvert :

        fs.close(fd, callback)

    Paramètres

        Voici la description des paramètres utilisés :

            *   fd − Il s'agit du descripteur de fichier renvoyé par la méthode fs.open() du fichier.
            *   callback − Il s'agit de la fonction de rappel. Aucun argument autre qu'une éventuelle exception n'est fourni au rappel d'achèvement.
        
    Exemple

        Créons un fichier js nommé main.js contenant le code suivant

            var fs = require("fs");

            var buf = new Buffer(1024);

            console.log("Going to open an existing file");

            fs.open('input.txt', 'r+', function(err, fd) {

                if (err) {
                    return console.error(err);
                }

                console.log("File opened successfully!");

                console.log("Going to read the file");

                fs.read(fd, buf, 0, buf.length, 0, function(err, bytes) {
                    
                    if (err) {
                        console.log(err);
                    }

                    // Print only read bytes to avoid junk.
                    
                    if(bytes > 0) {
                        console.log(buf.slice(0, bytes).toString());
                    }

                    // Close the opened file.
                    
                    fs.close(fd, function(err) {

                        if (err) {
                            console.log(err);
                        } 

                        console.log("File closed successfully.");
                    });
                });
            });

    Exécutez maintenant le main.js pour voir le résultat :

        $ node main.js

    Vérifiez la sortie :

        Going to open an existing file
        File opened successfully!
        Going to read the file
        Dummy Text For Testing !!!!!

        File closed successfully.


G-  Tronquer un fichier

    Syntaxe

    Voici la syntaxe de la méthode pour tronquer un fichier ouvert :

        fs.ftruncate(fd, len, callback)
    
    Paramètres
    
    Voici la description des paramètres utilisés :

        *   fd − Il s’agit du descripteur de fichier renvoyé par fs.open().

        *   len − Il s’agit de la longueur du fichier après laquelle le fichier sera tronqué.

        *   callback − Il s'agit de la fonction de rappel. Aucun argument autre qu'une éventuelle exception n'est fourni au rappel d'achèvement.
    
    Exemple
    
    Créons un fichier .js nommé main.js qui contient le code suivant :

        var fs = require("fs");
        var buf = new Buffer(1024);

        console.log("Going to open an existing file");
        fs.open('input.txt', 'r+', function(err, fd) {
        if (err) {
            return console.error(err);
        }
        console.log("File opened successfully!");
        console.log("Going to truncate the file after 10 bytes");
        
        // Truncate the opened file.
        fs.ftruncate(fd, 10, function(err) {
            if (err) {
                console.log(err);
            } 
            console.log("File truncated successfully.");
            console.log("Going to read the same file"); 
            
            fs.read(fd, buf, 0, buf.length, 0, function(err, bytes){
                if (err) {
                    console.log(err);
                }

                // Print only read bytes to avoid junk.
                if(bytes > 0) {
                    console.log(buf.slice(0, bytes).toString());
                }

                // Close the opened file.
                fs.close(fd, function(err) {
                    if (err) {
                    console.log(err);
                    } 
                    console.log("File closed successfully.");
                });
            });
        });
        });

    Exécutez maintenant le main.js pour voir le résultat

        $ node main.js
    
    Vérifier la sortie

        Going to open an existing file
        File opened successfully!
        Going to truncate the file after 10 bytes
        File truncated successfully.
        Going to read the same file
        Dummy Text 
        File closed successfully.


H-  Supprimer un fichier

    Syntaxe

    Voici la syntaxe de la méthode pour supprimer un fichier :

        fs.unlink(path, callback)
    
    Paramètres
    
    Voici la description des paramètres utilisés :

        *   chemin − Il s’agit du nom du fichier, y compris son chemin.

        *   callback − Il s'agit de la fonction de rappel. Aucun argument autre qu'une éventuelle exception n'est fourni au rappel d'achèvement.
    
    Exemple
    
    Créons un fichier .js nommé main.js contenant le code suivant

        var fs = require("fs");

        console.log("Going to delete an existing file");
        
        fs.unlink('input.txt', function(err) {

            if (err) {
                return console.error(err);
            }
            
            console.log("File deleted successfully!");
        
        });
    
    Exécutez maintenant le main.js pour voir le résultat

        $ node main.js
    
    Vérifier la sortie

        Going to delete an existing file
        File deleted successfully!


I-  Créer un répertoire

    Syntaxe

    Voici la syntaxe de la méthode pour créer un répertoire :

        fs.mkdir(path[, mode], callback)
    
    Paramètres
    
    Voici la description des paramètres utilisés :

        *   chemin − Il s’agit du nom du répertoire, y compris son chemin.

        *   mode − Il s'agit de l'autorisation de répertoire à définir. La valeur par défaut est 0777.

        *   callback − Il s'agit de la fonction de rappel. Aucun argument autre qu'une éventuelle exception n'est fourni au rappel d'achèvement.
    
    Exemple

    Créons un fichier .js nommé main.js contenant les éléments suivants :

    var fs = require("fs");

    console.log("Going to create directory /tmp/test");

    fs.mkdir('/tmp/test',function(err) {

        if (err) {
            return console.error(err);
        }

        console.log("Directory created successfully!");
    });

    Exécutez maintenant le main.js pour voir le résultat :

        $ node main.js

    Vérifiez la sortie :

        Going to create directory /tmp/test
        Directory created successfully!


J-  Lire un annuaire

    Syntaxe

    Voici la syntaxe de la méthode pour lire un répertoire :

        fs.readdir(path, callback)
    
    Paramètres
    
    Voici la description des paramètres utilisés :

    *   chemin − Il s’agit du nom du répertoire, y compris le chemin.
    
    *   callback − Il s'agit de la fonction de rappel qui reçoit deux arguments (err, files) où files est un tableau des noms des fichiers dans le répertoire à l'exclusion de '.' et '..'.
    
    Exemple
    
    Créons un fichier js nommé main.js contenant le code suivant :

    var fs = require("fs");

    console.log("Going to read directory /tmp");
    
    fs.readdir("/tmp/",function(err, files) {

        if (err) {
            return console.error(err);
        }
        
        files.forEach( function (file) {
            console.log( file );
        });

    });

    Exécutez maintenant le main.js pour voir le résultat :

        $ node main.js
    
    Vérifiez la sortie :

        Going to read directory /tmp
        ccmzx99o.out
        ccyCSbkF.out
        employee.ser
        hsperfdata_apache
        test
        test.txt


K-  Supprimer un répertoire

    Syntaxe

    Voici la syntaxe de la méthode pour supprimer un répertoire :

        fs.rmdir(path, callback)

    Paramètres
    
    Voici la description des paramètres utilisés :

    *   chemin − Il s’agit du nom du répertoire, y compris le chemin.

    *   callback − Il s'agit de la fonction de rappel. Aucun argument autre qu'une éventuelle exception n'est fourni au rappel d'achèvement.
    
    Exemple
    
    Créons un fichier .js nommé main.js contenant le code suivant :

        var fs = require("fs");

        console.log("Going to delete directory /tmp/test");

        fs.rmdir("/tmp/test",function(err) {

            if (err) {
                return console.error(err);
            }
            
            console.log("Going to read directory /tmp");
            
            fs.readdir("/tmp/",function(err, files) {
            
                if (err) {
                    return console.error(err);
                }
            
                files.forEach( function (file) {
                    console.log( file );
                });
            
            });
        
        });

    Exécutez maintenant le fichier main.js pour voir le résultat −

        $ node main.js
    
    Vérifiez la sortie.

        Going to read directory /tmp
        ccmzx99o.out
        ccyCSbkF.out
        employee.ser
        hsperfdata_apache
        test.txt