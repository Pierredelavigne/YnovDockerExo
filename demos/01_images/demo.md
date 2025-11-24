1. Rechercher une image sur DockerHub :

```bash
docker search ubuntu
```

2. Télécharger une image :

```bash
docker pull ubuntu:latest
```

3. Lister les images locales :

```bash
docker images
```

4. Inspecter une image :

```bash
docker inspect ubuntu:latest
```

5. Supprimer une image :

```bash
docker rmi hello-world:latest
```

- Possibilité de supprimer une image via l'id.

6. Tagger une image

```bash
docker tag ubuntu:latest ubuntu:my-tag
```
