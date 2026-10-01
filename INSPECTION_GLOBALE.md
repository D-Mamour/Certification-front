# Chantial Front — inspection globale Angular 22

## Architecture retenue

Le frontend utilise Angular 22 en composants standalone. L'état métier partagé repose sur les `signal()` et `computed()` des services :

- `AuthService` : session, profil, utilisateurs/bailleurs ;
- `ProjetService` : projets, étapes, avancements ;
- `FinanceService` : dépenses ;
- `DocumentService` : justificatifs, OCR et documents RAG ;
- `IntelligenceService` : analyses, anomalies et recommandations ;
- `InteractionService` : demandes, alertes et historique.

Les données métier ne sont pas simulées dans les espaces Entrepreneur, Bailleur et Administrateur : elles proviennent des endpoints Django.

## Corrections importantes

1. Les projets sont chargés dès l'ouverture de « Mes projets ». Le store est mis à jour dès que la réponse `/api/projets/` arrive.
2. Une création de projet est ajoutée immédiatement au signal `projetsSignal`.
3. « Ajouter une dépense » recharge projets + étapes dès l'ouverture. Si un seul projet/une seule étape existe, la sélection est automatique.
4. Le payload d'une dépense correspond au backend : `etape`, `libelle`, `montant`, `date_depense`, `fournisseur`.
5. Le justificatif est téléversé après création de la dépense, avec l'UUID de la dépense créée.
6. La liste des bailleurs vient de `/api/utilisateurs/` et n'utilise aucune liste statique.
7. Les sidebars lisent le profil depuis le signal `AuthService.utilisateur`.
8. Le JWT est ajouté automatiquement et un access token expiré est renouvelé via `/api/auth/rafraichir/`.
9. Les formulaires étape/avancement utilisent les API Angular 22 `input()` / `output()` et des formulaires réactifs.
10. Le graphique d'analyse factice a été remplacé par des indicateurs calculés à partir du budget, des dépenses et de l'avancement réels.
11. Les statistiques administrateur sont calculées depuis les vrais utilisateurs ; les nombres fictifs ont été supprimés.
12. La création administrateur d'un utilisateur demande désormais un mot de passe et envoie les rôles backend `ENTREPRENEUR`, `BAILLEUR`, `ADMINISTRATEUR`.
13. Les anciennes erreurs TS2729 d'initialisation des services ont été supprimées en utilisant `inject()` lorsque l'initialisation d'un champ dépend d'un service.
14. Les boutons « Consulter/Éditer » des dépenses mènent au projet concerné au lieu d'appeler des méthodes vides.
15. Les sélecteurs, compteurs, pagination et états vides reposent sur les données réellement chargées.

## Vérifications effectuées dans l'environnement de génération

- recherche globale des anciennes données métier factices : aucune occurrence des anciennes valeurs identifiées ;
- recherche des `console.log` de simulation : aucune occurrence ;
- vérification TypeScript statique sans résolution des paquets : aucune erreur interne restante, notamment aucune TS2729 ;
- correspondance des `formControlName` avec les formulaires réactifs revue ;
- endpoints comparés avec le backend Chantial fourni.

## Validation locale à faire

L'environnement de génération n'a pas pu télécharger les dépendances npm : `npm install` reste bloqué au niveau réseau. Le bundle Angular ne peut donc pas être certifié ici par `ng build`.

Sur la machine de développement :

```bash
npm install
ng build
ng serve
```

Le frontend attend Django sur `http://localhost:8000/api` et Angular sur `http://localhost:4200`.
