
![[2026_01_16_10_18__05 - Présentation projet professionnel.mp4]]

# Exposé – EL Habib

**Durée** : 35 min max (30–35 min)  
**Rythme** : 1 à 2 diapositives par partie  
**Support** : jointure tableau

---

## Plan

### 1. Entreprise Gemini

- Présentation du formateur / collègue
- Introduction du stage
- Présentation de Gemini => cacher ses données 
    - Protection des données
        - Santé
        - Militaire
        - Confidentialité / accès hors ligne

---

### 2. Explication du projet (sur 5 semaines)

- Compromis avec l’équipe sur les technologies
- Présentation du front-end à Bordeaux
- Diagramme de séquence
- Rendre + anonymes les données clients
- Chronologie du projet + Adaptation travail / formation

---
### 3. Travail du stagiaire

- Figma
- Front + API (cache licence)
- Maquettage de l’application
- Amélioration de l’expérience utilisateur (Front-end)
    - Mobile first
    - Cohérence avec l’application existante
    - Respect de la charte graphique Gemini

---
### 4. Organisation du travail

- GitHub + adaptation (GitLab)
    - Kanban
    - Méthode Agile
    - 1 branche Git par tâche

- Répartition des rôles
    - Stagiaire : Front-end
    - Maitre de stage : Back-end

--- 
## Environnement de travail

- Méthode Agile (explication)
- WordPress pour intégrer React (peu utilisé)
- Vite → configuration
- NPM → gestion des dépendances
- Axios → gestion des routes / requêtes
- IDE → VS Code

---

## Structure du projet

- React → architecture modulaire
- Interface multilingue
- Gestion des erreurs
    - Pop-ups
    - Boutons
    - Composants divers

---

## Interface statique

- Accessibilité => ARIA label
- Formulaires
- Code HTML

---

## Interface dynamique

- Possibilité de changer le format des données
- React pour manipuler et afficher les informations

---

## Configuration des appels API

- Axios
    - Création d’instances (API Gemini / Auth)

- Services API
    - Création de services pour les requêtes API
    - Paramètres
    - Corps de requête
    - Tokens

- Utilisation des services
    - Appels dynamiques
    - Intégration complète des requêtes

---

## Tests et gestion des erreurs

- Utilisation de la console navigateur
- Affichage de messages d’erreur personnalisés
- Mise en place de tests
    - Tests unitaires
    - Tests d’intégration (fichiers de test)

---

## Déploiement applicatif

- Surge → déploiement
- Utilisation de Docker

---

## Réalisations Back-end

- Microservice de gestion des utilisateurs (SaaS)
- Réutilisation du microservice dans d’autres projets
- Sortie des versions (Version de test  /=  Version finale)

---

## Conception de la base de données (back-end)

- MCD / MLD
- Relations et cardinalités
- Tables pivots
- Notion de clé étrangère
- Gestion du temps (TIME)

---

## Environnement de travail

- Méthode MERISE
- Utilisation de Looping
- IDE → IntelliJ IDEA
- Framework Java
- Maven

---

## Conception de l’API

- Inscription
- Ne pas stocker les données de l’utilisateur
    - (données conservées côté navigateur)
- Sécurisation par token
- Architecture évolutive et maintenable
- CRUD sur la table `users`

---

## Dictionnaire de données

- Typage
- Nom des champs
- Diagrammes UML
- Harmonisation des échanges Front / Back

---

## Mise en place de la base de données

- MariaDB
- Gestion des paramètres
- Requêtes préparées

---

### Réalisation structure MVC
- Bonne séparation des responsabilités
- Modularité
- Maintenabilité 

### Client application 
- Controller 
- Service
- Repository
- Modèle
- DB

### DTO (Data trasnfert Objet)
- Robustesse
- Sécurité
- Cohérence