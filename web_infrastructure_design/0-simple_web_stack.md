# Infrastructure Web Simple

Nous allons concevoir une infrastructure web simple en utilisant **1 serveur** qui héberge un site web accessible via le domaine `www.foobar.com`. Cette infrastructure sera basée sur les éléments suivants :

## Composants de l'Infrastructure

### 1. Serveur (avec une IP publique : 8.8.8.8)
Un serveur est une machine (physique ou virtuelle) qui exécute des services pour répondre aux demandes des utilisateurs. Dans ce cas, notre serveur héberge le site web.

### 2. Serveur Web (Nginx)
Le serveur web est chargé de :
- Traiter les requêtes HTTP/HTTPS des utilisateurs.
- Servir les fichiers statiques (comme des images ou du CSS).
- Transmettre les requêtes dynamiques à l’application.

### 3. Serveur d’Application
Le serveur d’application est responsable de :
- Exécuter le code de l’application (fichiers source).
- Générer les réponses dynamiques en fonction des requêtes des utilisateurs.

### 4. Base de Données (MySQL)
La base de données sert à :
- Stocker les informations nécessaires à l'application (par exemple : utilisateurs, articles, commandes).
- Permettre à l’application d’interagir pour lire ou modifier ces données.

### 5. Code Source (Code Base)
Le code source de l'application contient :
- La logique métier.
- Les fonctionnalités nécessaires pour répondre aux requêtes des utilisateurs.

### 6. Nom de Domaine (foobar.com)
Le nom de domaine, configuré avec un enregistrement DNS de type **A** (adresse), associe le nom `www.foobar.com` à l'adresse IP du serveur **8.8.8.8**.

---

## Détails sur les Rôles des Composants

### Le Serveur
- Héberge l’ensemble de l’infrastructure (serveur web, application, base de données).
- Reçoit les requêtes des utilisateurs et renvoie les réponses.

### Le Nom de Domaine (foobar.com)
- Simplifie l’accès au site web en utilisant un nom lisible (au lieu d’une IP).
- L’enregistrement DNS de type **A** associe `www.foobar.com` à l’adresse IP **8.8.8.8**.

### Le Serveur Web (Nginx)
- Sert les fichiers statiques (images, CSS, JavaScript).
- Redirige les requêtes dynamiques vers le serveur d’application.
- Gère les connexions utilisateur (HTTP/HTTPS).

### Le Serveur d’Application
- Traite les requêtes dynamiques.
- Exécute le code métier pour générer des réponses personnalisées.
- Interagit avec la base de données pour récupérer ou stocker des informations.

### La Base de Données (MySQL)
- Stocke les données structurées nécessaires à l’application.
- Permet un accès rapide et sécurisé aux informations.

### Communication avec l’Utilisateur
- Le serveur utilise **HTTP/HTTPS** pour communiquer avec le navigateur de l’utilisateur.
- HTTPS garantit la sécurité en cryptant les données échangées.

---

## Problèmes Potentiels (Issues)

### 1. SPOF (Single Point Of Failure)
- Toute l’infrastructure repose sur un seul serveur. Si ce serveur tombe en panne, tout le site devient inaccessible.

### 2. Temps d’Arrêt pendant la Maintenance
- Lorsque des modifications sont effectuées (comme déployer du nouveau code), le serveur web ou l'application doit être redémarré, provoquant une interruption temporaire.

### 3. Scalabilité Limitée
- Si le trafic augmente considérablement, un seul serveur ne pourra pas répondre à toutes les requêtes, entraînant des ralentissements ou des pannes.
