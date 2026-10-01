# Chantial — contrôle de présentation

## Parcours entrepreneur
1. Se connecter avec un compte ENTREPRENEUR actif.
2. La page Projets charge automatiquement `/api/projets/`, les étapes et les dépenses : aucun clic de rafraîchissement n'est nécessaire.
3. Créer un projet : la liste des bailleurs provient de `/api/utilisateurs/` et ne contient que les bailleurs actifs.
4. Ouvrir le projet, ajouter une étape, puis déclarer son avancement.
5. Aller dans Dépenses & justificatifs, ajouter une dépense et joindre une facture JPG/PNG/PDF.
6. Le backend crée le justificatif puis lance automatiquement l'OCR. Le store Angular ajoute immédiatement la dépense/justificatif.
7. Ouvrir Contrôle OCR : tous les résultats OCR accessibles sont sélectionnables ; le document réel peut être ouvert et l'OCR peut être relancé.
8. Dans Analyses, ajouter un document projet (devis/contrat), cliquer « Ajouter & indexer », puis lancer l'analyse IA/RAG.
9. Les notifications sont chargées automatiquement et peuvent être marquées comme lues.
10. Le profil est chargé depuis Django et la sidebar utilise le même signal utilisateur.

## Parcours bailleur
1. Se connecter avec le bailleur rattaché au projet.
2. Dashboard et Ma construction chargent automatiquement les projets, étapes, avancements, dépenses, anomalies et demandes.
3. Contrôle OCR affiche uniquement les justificatifs des projets du bailleur.
4. Valider/rejeter une dépense crée une alerte pour l'entrepreneur.
5. Envoyer une demande crée une alerte pour son destinataire.

## Parcours administrateur
1. La liste des utilisateurs et l'historique sont chargés depuis l'API.
2. Activation/désactivation utilise les valeurs backend `ACTIF` / `INACTIF`.
3. Aucune donnée métier de démonstration n'est codée en dur dans les composants.

## Contrôles effectués dans l'environnement de génération
- Compilation syntaxique Python : OK (`python -m compileall`).
- Recherche des anciens `ChantialApiService` / `this.api` : aucune référence.
- Recherche de handlers `(click)` sans méthode TypeScript correspondante : 0.
- Recherche des anciennes données fictives connues (noms, projets, montants) : aucune occurrence.
- Installation npm impossible à terminer dans l'environnement isolé ; `ng build` doit donc être exécuté sur la machine de présentation après `npm install`.
