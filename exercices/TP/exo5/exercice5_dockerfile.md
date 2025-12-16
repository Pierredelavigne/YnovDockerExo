# Énoncé — Dockeriser une application Java (multi-stage) et publier l’image sur Docker Hub

## Contexte

Vous disposez d’une application Java (ex. Spring Boot) hébergée sur GitHub. L’objectif est de produire une image Docker **optimisée** via un **Dockerfile multi-stage** (build séparé du runtime), puis de **publier** cette image sur **Docker Hub**.

Si vous n’avez pas de dépôt public sous la main, vous pouvez partir d’un projet Spring Boot “Hello World” de votre choix (ou générer un projet minimal via Spring Initializr), puis le pousser sur GitHub.

---

## Objectifs attendus

1. Construire l’application Java dans une étape dédiée (“builder stage”).
2. Créer une image finale **légère** qui ne contient que le nécessaire pour exécuter l’application.
3. Lancer un conteneur et vérifier que l’application répond correctement.
4. Tagger l’image et la **push** sur Docker Hub.



## Livrables

1. Le fichier `Dockerfile` (multi-stage).
2. Les commandes utilisées pour :
   * build l’image
   * run le conteneur
   * tagger l’image
   * push l’image sur Docker Hub
3. L’URL Docker Hub du repository contenant l’image publiée.

## Étapes réalisées

### 1. Création du projet Spring Boot
- Génération d’un projet via Spring Initializr
- Configuration : Maven, Java 17, packaging JAR
- Ajout de la dépendance Spring Web
- Création d’un endpoint HTTP simple (`/`) pour tester l’application

---

### 2. Test de l’application en local

```bash
./mvnw spring-boot:run
```

```bash
curl http://localhost:8080
```

---

### 3. Dockerfile multi-stage

```dockerfile
# ===== Builder stage =====
FROM maven:3.9-eclipse-temurin-21 AS builder
WORKDIR /app

COPY pom.xml .
COPY .mvn .mvn
COPY mvnw mvnw
RUN chmod +x mvnw
RUN ./mvnw -DskipTests dependency:go-offline

COPY src src
RUN ./mvnw -DskipTests clean package

# ===== Runtime stage =====
FROM eclipse-temurin:21-jre
WORKDIR /app

COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
```

---

## Commandes utilisées

### Build de l’image Docker

```bash
docker build -t spring-hello:1.0 .
```

### Lancement du conteneur

```bash
docker run -p 8080:8080 spring-hello:1.0
```

### Authentification Docker Hub

```bash
docker login
```

### Tag de l’image

```bash
docker tag spring-hello:1.0 stonelight/spring-hello:1.0
docker tag spring-hello:1.0 stonelight/spring-hello:latest
```

### Publication sur Docker Hub

```bash
docker push stonelight/spring-hello:1.0
docker push stonelight/spring-hello:latest
```

### Test d’une image Docker distante

```bash
docker pull lucasvanv/exo5:latest
docker run -p 8082:8080 lucasvanv/exo5:latest
```

Test via navigateur ou Postman :

```text
http://localhost:8082/add
```

---

## URL Docker Hub

https://hub.docker.com/r/stonelight/spring-hello

---

## Conclusion

Ce TP a permis de mettre en pratique la création d’un Dockerfile multi-stage, la construction d’une image Docker Java optimisée, le déploiement d’un conteneur ainsi que la publication et le test d’images sur Docker Hub.