
# Service de Gestion des Cotes
Ceci est une application Flask simple qui sert de service de gestion des cotes (notes) pour des étudiants. Elle permet d'initialiser un espace pour un étudiant, d'ajouter des notes et de récupérer les notes existantes pour un étudiant donné.

## Fonctionnalités

*   **Initialisation d'étudiant** : Crée une entrée en mémoire pour un nouvel étudiant (généralement notifié par le service d'inscription).
*   **Ajout de notes** : Permet d'ajouter une note à la liste des notes d'un étudiant existant.
*   **Récupération des notes** : Renvoie le nom et la liste des notes d'un étudiant spécifique.

## Prérequis

*   Python 3.9
*   pip (gestionnaire de paquets Python)

## Installation

1.  Clonez le dépôt ou copiez le fichier `grades_service.py`.
2.  Installez les dépendances nécessaires :
    ```bash
    pip install -r requirements.txt
    ```

## Lancement de l'application

1.  Placez-vous dans le répertoire contenant le fichier `service_cotes.py`.
2.  Exécutez la commande suivante dans votre terminal :
    ```bash
    python grades_service.py
    ```
3.  Le service sera lancé et accessible à l'adresse `http://localhost:5001` (ou l'adresse IP de votre machine sur le port 5001).

## Endpoints de l'API

*   **`POST /init_student`**
    *   **Description** : Initialise un enregistrement pour un étudiant dans le système de notes.
    *   **Corps de la requête (JSON)** :
        ```json
        {
          "id": <id_de_l_etudiant>,
          "name": "Nom de l'étudiant"
        }
        ```
    *   **Réponse (Succès - 200)** :
        ```json
        {
          "message": "Espace notes créé pour <Nom de l'étudiant>"
        }
        ```

*   **`POST /add_grade/<student_id>`**
    *   **Description** : Ajoute une note pour l'étudiant spécifié par `<student_id>`.
    *   **Corps de la requête (JSON)** :
        ```json
        {
          "grade": <valeur_de_la_note>
        }
        ```
        *(Note : La `<valeur_de_la_note>` peut être un nombre ou une chaîne de caractères, selon ce que vous souhaitez stocker).*
    *   **Réponse (Succès - 200)** :
        ```json
        {
          "message": "Note ajoutée"
        }
        ```
    *   **Réponse (Erreur - 404)** : Si l'étudiant avec l'ID `<student_id>` n'a pas été initialisé.
        ```json
        {
          "error": "Etudiant non trouvé"
        }
        ```

*   **`GET /get_grades/<student_id>`**
    *   **Description** : Récupère le nom et la liste des notes pour l'étudiant spécifié par `<student_id>`.
    *   **Réponse (Succès - 200)** :
        ```json
        {
          "name": "Nom de l'étudiant",
          "grades": [ <note1>, <note2>, ... ]
        }
        ```
    *   **Réponse (Erreur - 404)** : Si l'étudiant avec l'ID `<student_id>` n'a pas été initialisé.
        ```json
        {
          "error": "Etudiant non trouvé"
        }
        ```
    *`GET /get_all_grades`**
    *   **Description** : Récupère la liste de tous les étudiants et leurs notes.
    *   **Réponse (Succès - 200)** :
        ```json
        {
          "students": [
            {
              "id": <id_de_l_etudiant>,
              "name": "Nom de l'étudiant",
              "grades": [ <note1>, <note2>, ... ]
            },
            ...
          ]
        }
        ```
