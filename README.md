# Student List - Projet Docker (POZOS)

Projet réalisé par Dolly Ongmanak dans le cadre du stage DevOps chez EazyTraining.

## Description
Application composée d'une API Python/Flask exposant une liste d'étudiants avec leur âge,
et d'un site web PHP consommant cette API, le tout conteneurisé avec Docker.

## 1. Build et test de l'API

Commande de build :
docker build -t student_list:v1 .

Test de l'API avec authentification :
curl -u toto:python -X GET http://localhost:5000/pozos/api/v1.0/get_student_ages

Test de l'API seule via curl sur le port 5000, avec authentification.
La reponse JSON confirme que l'API Flask fonctionne correctement et retourne
la liste des etudiants avec leur age.

[CAPTURE 1 ICI]

## 2. Deploiement avec docker-compose

Commande de lancement :
docker-compose up -d

Site web accessible sur le port 8080 apres deploiement via docker-compose.
La page affiche correctement la liste des etudiants recuperee depuis l'API,
ce qui confirme la communication entre les deux conteneurs via le reseau
Docker pozos_network.

[CAPTURE 2 ICI]

## 3. Registre prive Docker

Commandes :
docker run -d -p 5001:5000 --name registry registry:2
docker tag student_list:v1 localhost:5001/student_list:v1
docker push localhost:5001/student_list:v1
curl http://localhost:5001/v2/_catalog

Verification du registre Docker prive deploye localement (port 5001).
Le catalogue confirme que l'image student_list a bien ete poussee et est
disponible dans le registre.

[CAPTURE 3 ICI]

## Fichiers du projet
- simple_api/Dockerfile : construit l'image de l'API
- docker-compose.yml : orchestre les services website et api

## Auteur
Dolly Ongmanak
