1. Télécharger une image :

```bash
docker pull ubuntu:latest
```

2. Exécuter un conteneur :

- Utilisez la commande `docker run` pour créer et demarrer un conteneur basé sur l'image ubuntu :

```bash
docker run -it ubuntu:latest
```

- it : Ces options permettent d'exécuter le conteneur en mode interactif.
- ubuntu:latest : Le nom de l'image que vous voulez utiliser.

3. Mettre à jour les paquets à l'intérieur du conteneur :

```bash
apt update
apt upgrade
```

4. Installer un outils à l'intérieur de notre coneneur :

```bash
apt install nano
```

5. Sortir du conteneur :

- Pour sortir du conteneur tout en laissant en cours d'exécution, utilisez ctrl + p puis ctrl + q ou tapez exit dans le conteneur.
