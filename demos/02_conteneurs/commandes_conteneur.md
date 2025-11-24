# Les commandes pour les conteneurs

1. **Lancer un conteneur** :

   ```bash
   docker run [options] IMAGE [COMMAND] [ARG...]
   ```

   - Exemple : `docker run -d -p 80:80 nginx` (lance un conteneur nginx en arrière-plan et mappe le port 80).

2. **Lister les conteneurs** :

   ```bash
   docker ps [options]
   ```

   - Exemple : `docker ps -a` (affiche tous les conteneurs, y compris ceux qui sont arrêtés).

3. **Arrêter un conteneur** :

   ```bash
   docker stop [CONTAINER]
   ```

   - Exemple : `docker stop mon_conteneur` (arrête le conteneur nommé "mon_conteneur").

4. **Démarrer un conteneur arrêté** :

   ```bash
   docker start [CONTAINER]
   ```

   - Exemple : `docker start mon_conteneur`.

5. **Redémarrer un conteneur** :

   ```bash
   docker restart [CONTAINER]
   ```

   - Exemple : `docker restart mon_conteneur`.

6. **Supprimer un conteneur** :

   ```bash
   docker rm [CONTAINER]
   ```

   - Exemple : `docker rm mon_conteneur` (supprime le conteneur après qu'il soit arrêté).

7. **Voir les logs d'un conteneur** :

   ```bash
   docker logs [CONTAINER]
   ```

   - Exemple : `docker logs mon_conteneur`.

8. **Exécuter une commande dans un conteneur actif** :

   ```bash
   docker exec [options] CONTAINER COMMAND [ARG...]
   ```

   - Exemple : `docker exec -it mon_conteneur bash` (ouvre une session bash dans le conteneur).

9. **Inspecter un conteneur** :

   ```bash
   docker inspect [CONTAINER]
   ```

   - Exemple : `docker inspect mon_conteneur` (fournit des détails détaillés sur le conteneur).

10. **Afficher les statistiques de l'utilisation des ressources par les conteneurs** :
    ```bash
    docker stats
    ```
    - Exemple : `docker stats` (affiche les statistiques en temps réel pour tous les conteneurs en cours).
