# StuDay: Créer des diagrammes via code

## Sujet

Paris sportifs:

* Consulter l'offre de paris

## Diagramme de cas d'utilisation

En tant que joueur, je peux consulter l'offre de paris pour pouvoir poser un pari.

```mermaid
sequenceDiagram
    participant Joueur
    participant Application
    participant Catalogue
    Joueur ->> Application: Consulter l'offre de paris
    Application ->> Catalogue: GET /offers
    activate Catalogue
    Catalogue ->> Application: Résultat de la requête
    deactivate Catalogue
```

En tant que Catalogue, je peux répondre à une requête de consultation de l'offre de paris.

```mermaid
sequenceDiagram
    participant Application
    participant Catalogue
    participant Fournisseur
    participant Trader
    Fournisseur -->> Catalogue: Notifie de la mise à jour de l'offre
    Trader -->> Catalogue: Notifie d'un changement de cote
    Catalogue ->> Catalogue: Traite l'offre
    alt Offre mise à jour
        Catalogue ->> Catalogue: Met à jour l'offre en cache
        Catalogue -->> Application: Notifie de la mise à jour de l'offre
    else Offre inchangée
        note right of Catalogue: Ne fait rien
    end
```

## Représentation des données

```mermaid
classDiagram
    class BetOffer {
        +id: int
        +name: string
        +description: string
        +odds: float
        +status: string
        +result: string
        +date: date
        +isAvailable() bool
    }
    class FootballBetOffer {
        +team1: string
        +team2: string
    }
    class TennisBetOffer {
        +player1: string
        +player2: string
    }
    BetOffer <|-- FootballBetOffer
    BetOffer <|-- TennisBetOffer
```

## Répresentation de l'état de l'offre

```mermaid
stateDiagram
    [*] --> Disponible
    state "En attente" as EnAttente
    Disponible --> EnAttente: N'accepte pas de pari
    Disponible --> Annulé: Offre annulée<br/>ou supprimée
    Annulé --> [*]
    EnAttente --> Disponible: Accepte les paris
    Disponible --> Terminé: Résultat connu
    EnAttente --> Terminé: Résultat connu
    Terminé --> [*]
```

## Ouvrir une PR sur GitHub 

GitHub est capable d'afficher les diagrammes Mermaid

## Importer le diagramme sur Draw.io

Draw.io est capable d'importer (mais pas d'exporter) les diagrammes Mermaid

## (Re)parler de l'avantage de Mermaid avec GitHub Copilot

Assistance à la création des diagrammes (syntaxe Mermaid) et fonctionnel 

## Conclusion

* Prise en main rapide
  * Intégré à l'IDE
  * Assistance GitHub Copilot
* Multiples types de diagrammes
  * Séquence
  * Classe
  * État
  * Flow
* Import Draw.io
* Visualisation GitHub

## Évoquer les limitations

* Design basique
* Pas d'image
* Pas de bibliothèque d'icônes pour les diagrammes d'architecture (AWS, Azure, etc.)

## Évoquer les alternatives

Diagram propose une alternative pour créer ses diagrammes d'architecture
* [Diagrams](https://diagrams.mingrammer.com/docs/getting-started/examples) en Python (ou en Go)

