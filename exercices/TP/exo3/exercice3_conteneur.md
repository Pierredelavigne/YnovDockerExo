# TP conteneur

## Partie 1

- En utilisant votre machine Windows, lancez le service Docker, s’il n’est pas lancé.

- Créer une image Docker sur votre machine du jeu 2048 (voir screen jeux_2048).

- Vérifier que l’image est bien présente sur votre machine.

- Lancer ce jeu sur un port disponible au travers d’un conteneur que vous allez appeler «jeu-votre-nom ». 

- Vérifier que le conteneur est bien lancé avec la commande adaptée.

- Créer un second conteneur qui va lancer le même jeu mais avec un nom différent «jeu2-votre-nom ».

- Les 2 jeux sont fonctionnels en même temps sur votre machine, effectuez la commande pour vérifier la présence des conteneurs.

- Ouvrez les 2 jeux sur votre navigateur. 

- Stopper les 2 conteneurs et assurez-vous que ces 2 conteneurs sont arrêtés.

- Relancez le conteneur «jeu2-votre-nom » et aller vérifier dans votre navigateur s’il fonctionne bien. Effectuez la commande pour voir s’il a bien été relancé. Puis stopper le. 

- Supprimez l’image du jeu 2048 et les conteneurs associés.

- Vérifiez que les suppressions ont bien été faite.


``` bash
# 1. Cloner le code source du jeu 2048
git clone https://github.com/gabrielecirulli/2048.git

# 2. Créer le Dockerfile dans le dossier 2048
cd 2048
nano Dockerfile
# → Contenu du Dockerfile :
#   FROM nginx:alpine
#   COPY . /usr/share/nginx/html

# 3. Construire l’image Docker
docker build -t 2048-game .

# 4. Vérifier que l’image existe
docker images

# 5. Lancer le premier conteneur (port 8080)
docker run -d --name jeu-pierre -p 8080:80 2048-game

# 6. Lancer le second conteneur (port 8081)
docker run -d --name jeu2-pierre -p 8081:80 2048-game

# 7. Vérifier que les deux conteneurs tournent
docker ps

# 8. Arrêter les deux conteneurs
docker stop jeu-pierre jeu2-pierre

# 9. Vérifier qu’ils sont arrêtés
docker ps      # Ne doit plus rien afficher
docker ps -a   # Statut Exited pour les deux

# 10. Relancer le conteneur 'jeu2-pierre'
docker start jeu2-pierre

# 11. Vérifier qu’il est bien relancé
docker ps

# 12. Arrêter à nouveau 'jeu2-pierre'
docker stop jeu2-pierre

# 13. Supprimer les deux conteneurs
docker rm jeu-pierre jeu2-pierre

# 14. Supprimer l’image Docker
docker rmi 2048-game

# 15. Vérifier la suppression
docker images        # « 2048-game » ne doit plus apparaître
docker ps -a         # Les conteneurs ne doivent plus apparaître
```


## Partie 2


- Récupérer une image docker nginx.

- Créer un conteneur en vous basant sur cette image en lui attribuant le nom suivant : « nginx-web».

- Assurez-vous que l’image est bien présente et que le conteneur est bien lancé.

- Ce serveur nginx web (nginx-web) devra être lancé sur un port disponible.

- Vérifier que le serveur est bien lancé au travers du navigateur.

- Une page web avec «Welcome to nignx » devrait s'afficher (voir nginx.png). 

- Effectuer la commande vous permettant de rentrer à l’intérieur de votre serveur nginx.

- Une fois à l’intérieur, aller modifier la page html par défaut de votre serveur nginx en changeant le titre de la page en :  
Welcome «votre prenom ».

- Relancez votre serveur et assurez-vous que le changement à bien été pris en compte, en relançant votre navigateur.

- Refaite la même opération mais en utilisant le serveur web apache et donc il faudra créer un autre conteneur.

- Il faut supprimer le contenu complet de l'index.html et y mettre : "Je suis heureux et je m'appelle votre prenom".

- Le changement doit appaître dans votre navigateur.

```bash 
# 1. Récupérer l’image Nginx
docker pull nginx

# 2. Créer et lancer le conteneur sur un port (ex : 8082)
docker run -d --name nginx-web -p 8082:80 nginx

# 3. Vérifier image et conteneur
docker images
docker ps

# 4. Tester dans le navigateur
# Accéder à http://localhost:8082

# 5. Entrer dans le conteneur
docker exec -it nginx-web /bin/sh

# 6. Modifier la page d'accueil
echo '<h1>Welcome "Pierre"</h1>' > /usr/share/nginx/html/index.html

# 7. Relancer le serveur
docker restart nginx-web

# 8. Vérifier la modification dans le navigateur
# Accéder à http://localhost:8082
```

```bash
# 1. Récupérer l’image Apache
docker pull httpd

# 2. Créer et lancer le conteneur sur un port (ex : 8083)
docker run -d --name apache-web -p 8083:80 httpd

# 3. Vérifier image et conteneur
docker images
docker ps

# 4. Entrer dans le conteneur
docker exec -it apache-web /bin/bash

# 5. Modifier la page d'accueil
echo "Je suis heureux et je m'appelle Pierre" > /usr/local/apache2/htdocs/index.html

# 6. Relancer le serveur
docker restart apache-web

# 7. Vérifier la modification dans le navigateur
# Accéder à http://localhost:8083
```

## Partie 3


- Répétez 3 fois la même opération que pour le début de la partie 2, il faudra juste appelez vos conteneurs :

- « nginx-web3 ».

- « nginx-web4 ».

- « nginx-web5 ».

- Il faudra faire en sorte que les pages html présente dans les fichiers ci-dessous s’affiche dans chacun des navigateurs en lien avec vos conteneurs :

- html5up-editorial-m2i.zip pour nginx-web3

- html5up-massively.zip pour nginx-web4

- html5up-paradigm-shift.zip pour nginx-web5

- Stopper, ensuite, ces différents conteneurs.
```bash
unzip html5up-editorial-m2i.zip -d ./editorial
unzip html5up-massively.zip -d ./massively
unzip html5up-paradigm-shift.zip -d ./paradigm-shift

chmod -R 755 ./editorial/html5up-editorial
chmod -R 755 ./massively
chmod -R 755 ./paradigm-shift

docker run -d --name nginx-web3 -p 8084:80 -v $(pwd)/editorial/html5up-editorial:/usr/share/nginx/html:Z nginx
docker run -d --name nginx-web4 -p 8085:80 -v $(pwd)/massively:/usr/share/nginx/html:Z nginx
docker run -d --name nginx-web5 -p 8086:80 -v $(pwd)/paradigm-shift:/usr/share/nginx/html:Z nginx


http://localhost:8084 pour nginx-web3 (editorial)

http://localhost:8085 pour nginx-web4 (massively)

http://localhost:8086 pour nginx-web5 (paradigm-shift)

docker stop nginx-web3 nginx-web4 nginx-web5

```