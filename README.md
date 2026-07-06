# Student List - Projet Docker

Projet réalisé par Dolly Ongmanak dans le cours introduction au DevOps chez EazyTraining.

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

<img width="1200" height="239" alt="MyScreen7_6_2026_12_27_11_PM" src="https://github.com/user-attachments/assets/b233209b-7e53-4503-876d-9ebf8274d1d7" />


## 2. Deploiement avec docker-compose

Commande de lancement :
docker-compose up -d

Site web accessible sur le port 8080 apres deploiement via docker-compose.
La page affiche correctement la liste des etudiants recuperee depuis l'API.

<img width="1200" height="271" alt="MyScreen7_6_2026_12_02_41_PM" src="https://github.com/user-attachments/assets/70f3f0c4-c1d7-4b80-9644-074ce41e24da" />

## 3. Verification que les conteneurs sont actifs
docker ps

Verification avec docker ps que les deux conteneurs (website et api) sont bien
demarres et actifs apres le lancement de docker-compose up -d.

<img width="1200" height="188" alt="MyScreen7_6_2026_12_28_35_PM" src="https://github.com/user-attachments/assets/06f9c119-af53-4dd1-ad09-9e5815707200" />


## 4. Registre prive Docker

Commandes :
docker run -d -p 5001:5000 --name registry registry:2
docker tag student_list:v1 localhost:5001/student_list:v1
docker push localhost:5001/student_list:v1
curl http://localhost:5001/v2/_catalog

La capture confirme que l'image student_list a bien ete poussee et est
disponible dans le registre.

<img width="1200" height="160" alt="MyScreen7_6_2026_12_29_41_PM" src="https://github.com/user-attachments/assets/b4e5b0e8-f759-415f-826e-4c8c35f062fc" />


## Fichiers du projet
- simple_api/Dockerfile : construit l'image de l'API
- docker-compose.yml : orchestre les services website et api

## Auteur
Dolly Ongmanak
