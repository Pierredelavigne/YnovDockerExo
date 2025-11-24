# Commandes Docker pour les Images

## Rechercher une Image

Pour rechercher une image sur Docker Hub :

```bash
docker search <image_name>
```

Exemple :

```bash
docker search ubuntu
```

## Télécharger une Image

Pour télécharger une image depuis Docker Hub :

```bash
docker pull <image_name>:<tag>
```

Exemple :

```bash
docker pull ubuntu:latest
```

## Lister les Images Locales

Pour voir toutes les images que tu as téléchargées localement :

```bash
docker images
```

## Supprimer une Image

Pour supprimer une image de ton système :

```bash
docker rmi <image_name>:<tag>
```

Exemple :

```bash
docker rmi ubuntu:latest
```

Si l'image est utilisée par un conteneur (même arrêté), tu peux forcer la suppression avec `-f` :

```bash
docker rmi -f <image_name>:<tag>
```

## Inspecter une Image

Pour obtenir des détails sur une image :

```bash
docker inspect <image_name>:<tag>
```

Exemple :

```bash
docker inspect ubuntu:latest
```

## Tagger une Image

Pour ajouter un tag à une image :

```bash
docker tag <existing_image>:<existing_tag> <new_image>:<new_tag>
```

Exemple :

```bash
docker tag ubuntu:latest ubuntu:my-tag
```

## Pousser une Image vers un Registre

Pour pousser une image locale vers Docker Hub ou un autre registre Docker :

```bash
docker push <image_name>:<tag>
```

Exemple :

```bash
docker push myrepo/myimage:latest
```

## Sauvegarder une Image

Pour sauvegarder une image dans un fichier tarball :

```bash
docker save -o <path_to_output_file> <image_name>:<tag>
```

Exemple :

```bash
docker save -o ubuntu_latest.tar ubuntu:latest
```

## Charger une Image

Pour charger une image à partir d'un fichier tarball :

```bash
docker load -i <path_to_input_file>
```

Exemple :

```bash
docker load -i ubuntu_latest.tar
```

## Historique d'une Image

Pour voir l'historique des couches d'une image :

```bash
docker history <image_name>:<tag>
```

Exemple :

```bash
docker history ubuntu:latest
```

## Supprimer les Images Dangling

Pour supprimer les images intermédiaires non utilisées (dangling) :

```bash
docker image prune
```

## Supprimer Toutes les Images

Pour supprimer toutes les images de ton système :

```bash
docker rmi $(docker images -q)
```

**Remarque :** Cette commande supprimera toutes les images locales, utilise-la avec prudence.
