1. Pourquoi utilisons-nous une table Oeuvre séparée des tables Film et Serie? Quels sont les avantages de cette structure?
2. Comment le modèle gère-t-il le cas où une personne est à la fois acteur et réalisateur dans le même film?
3. Expliquez pourquoi la relation entre Oeuvre et Recompense est `}o--o|` plutôt que `||--o{`. Quelle différence cela fait-il?
4. Comment pourriez-vous modifier ce modèle pour prendre en compte les franchises de films (comme Marvel Cinematic Universe ou Star Wars)?
5. Dans ce modèle, comment retrouver tous les films dans lesquels un acteur a joué avec un autre acteur spécifique?
6. Pourquoi avons-nous besoin d'une table Participation séparée au lieu de créer simplement une relation directe entre Personne et Oeuvre?
7. Comment ce modèle gère-t-il les remakes ou les adaptations d'œuvres existantes?
8. Si nous voulions ajouter un système de recommandation basé sur les préférences des utilisateurs, quelles tables devrions-nous ajouter au modèle?

erDiagram
    Utilisateur {
        id INT PK
        pseudo STRING
        email STRING
        date_inscription DATE
    }
    Critique {
        id INT PK
        oeuvre_id INT FK
        utilisateur_id INT FK
        note INT
        commentaire TEXT
        date_publication DATE
    }
    Oeuvre {
        id INT PK
        titre STRING
        annee_sortie INT
        synopsis TEXT
        pays_origine STRING
        classification_age STRING
        type STRING
    }
    Film {
        id INT PK
        oeuvre_id INT FK
        duree INT
        budget DECIMAL
        recettes DECIMAL
    }
    Serie {
        id INT PK
        oeuvre_id INT FK
        nb_saisons INT
        statut STRING
    }
    Episode {
        id INT PK
        serie_id INT FK
        saison INT
        numero INT
        titre STRING
        duree INT
        date_diffusion DATE
    }
    Oeuvre_Genre {
        oeuvre_id INT FK
        genre_id INT FK
    }
    Genre {
        id INT PK
        nom STRING
        description STRING
    }
    Participation {
        id INT PK
        personne_id INT FK
        oeuvre_id INT FK
        role STRING
        type_participation STRING
        personnage STRING
    }
    Personne {
        id INT PK
        nom STRING
        prenom STRING
        date_naissance DATE
        nationalite STRING
        biographie TEXT
    }
    Recompense {
        id INT PK
        nom STRING
        annee INT
        categorie STRING
        oeuvre_id INT FK
        personne_id INT FK
    }
    
    Utilisateur ||--o{ Critique : "écrit"
    Critique }|--|| Oeuvre : "concerne"
    Oeuvre ||--o| Film : "est un"
    Oeuvre ||--o| Serie : "est une"
    Serie ||--o{ Episode : "contient"
    Oeuvre ||--o{ Oeuvre_Genre : "est classé dans"
    Oeuvre_Genre }|--|| Genre : "fait référence à"
    Oeuvre ||--o{ Participation : "implique"
    Participation }|--|| Personne : "concerne"
    Oeuvre |o--o{ Recompense : "peut remporter"
    Personne |o--o{ Recompense : "peut remporter"

