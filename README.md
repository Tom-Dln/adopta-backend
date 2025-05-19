
# 📦 Adopta'Compagnon – Backend Strapi

Bienvenue dans le dépôt backend de l’application **Adopta'Compagnon**, développée avec **Strapi**.
Ce backend gère les données liées aux animaux, refuges, types d’animaux et demandes d’adoption.  
Il expose une API REST consommée par le frontend Vue.js pour permettre aux utilisateurs de consulter les profils d’animaux et envoyer une demande d’adoption.

---

## 🚀 Lancer le projet en local

1. Cloner le dépôt :
```bash
git clone https://github.com/Tom-Dln/adopta-backend.git
cd adopta-backend
```

2. Installer les dépendances :
```bash
npm install
```

3. Lancer Strapi :
```bash
npm run develop
```

Par défaut, Strapi démarre sur `http://localhost:1337`.  
L’interface d’administration est disponible à cette adresse pour gérer les contenus.

---

## 🗂️ Structure des collections (modèles Strapi)

### 1. 🐾 `Animal`
| Champ        | Type     | Description                                 |
|--------------|----------|---------------------------------------------|
| name         | String   | Nom de l’animal                             |
| documentId   | UID      | Identifiant unique pour accès par l'API     |
| age          | Number   | Âge de l’animal (en années)                 |
| description  | Text     | Présentation ou comportement                |
| breed        | String   | Race ou croisement                          |
| size         | Enum     | Taille : `small`, `medium`, `large`         |
| sterilized   | Boolean  | Indique si l’animal est stérilisé           |
| adopted      | Boolean  | Statut d’adoption                           |
| photo        | Media    | Image principale                            |
| type         | Relation | `many-to-one` vers `Type`                   |
| shelter      | Relation | `many-to-one` vers `Shelter`                |

### 2. 🧬 `Type`
| Champ      | Type     | Description              |
|------------|----------|--------------------------|
| name       | String   | Espèce (chien, chat...)  |
| documentId | UID      | Identifiant unique       |

### 3. 🏠 `Shelter`
| Champ          | Type     | Description                     |
|----------------|----------|---------------------------------|
| name           | String   | Nom du refuge                   |
| address        | String   | Adresse complète                |
| phone          | String   | Téléphone du refuge             |
| contact_email  | Email    | Email de contact                |
| website        | String   | Site internet (sans https)      |
| documentId     | UID      | Identifiant unique              |

### 4. 📝 `AdoptionRequest`
| Champ          | Type      | Description                             |
|----------------|-----------|-----------------------------------------|
| full_name      | String    | Nom et prénom du demandeur              |
| email          | Email     | Adresse mail du demandeur               |
| phone          | String    | Numéro de téléphone                     |
| message        | Text      | Message personnalisé                    |
| request_status | Enum      | État de la demande (`pending`, etc.)    |
| animal         | Relation  | Animal concerné (vers `Animal`)         |

---

## 🧩 Schéma relationnel

```
[Shelter] 1---* [Animal] *---1 [Type]
                    |
                    *---1 [AdoptionRequest]
```

- Un `Shelter` possède plusieurs `Animals`
- Un `Type` peut être partagé entre plusieurs animaux
- Une `AdoptionRequest` est liée à **un seul** `Animal`

---

## 🔁 Routes API utilisées

### 🔹 `Animal`
- `GET /api/animals` — liste des animaux
- `GET /api/animals/:id` — détail d’un animal
- `GET /api/animals?filters[documentId][$eq]=...&populate=*`

### 🔹 `Shelter`
- `GET /api/shelters` — liste des refuges

### 🔹 `Type`
- `GET /api/types` — liste des types d’animaux

### 🔹 `AdoptionRequest`
- `POST /api/adoption-requests` — envoi d'une demande
- Champs : `full_name`, `email`, `phone`, `message`, `animal`, `request_status`

---

## 🧑‍💻 Technologies
- **Strapi** v4
- **SQLite** (développement)
- API REST + Interface Admin intégrée

---

## 📝 Auteur

Tom Delaunay | MyDigitalSchool Caen | M2-DFS 2025
