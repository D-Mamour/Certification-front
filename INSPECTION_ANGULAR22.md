# Chantial Front — inspection Angular 22

## Corrections structurantes
- Les projets, étapes et avancements sont maintenant stockés dans des `signal()` dans `ProjetService`.
- Les dépenses sont stockées dans un `signal()` dans `FinanceService`.
- Les agrégats (nombre de projets, total dépenses, cartes projet) utilisent `computed()`.
- Après création d'un projet, d'une étape, d'un avancement ou d'une dépense, le signal correspondant est mis à jour immédiatement : aucun clic de rafraîchissement n'est nécessaire.
- La page « Mes projets » charge ses données dès `ngOnInit` et affiche les projets dès la réponse API.
- Le formulaire « Ajouter une dépense » recharge projets + étapes à son ouverture et filtre les étapes avec un `computed()` selon le projet sélectionné.
- Le formulaire bloque explicitement une dépense si le projet ne possède aucune étape et affiche le message d'erreur Django en français.
- Le champ « Catégorie » a été retiré du formulaire de dépense car il n'existe pas dans le modèle Django `Depense`.
- « Description détaillée » a été aligné sur le champ backend `fournisseur`.
- Le justificatif reste facultatif ; s'il est fourni, il est envoyé après création de la dépense.
- La liste des bailleurs est issue de `/api/utilisateurs/`, sans données fictives.
- `AuthService` expose maintenant également `utilisateursSignal` ; le nom du bailleur est résolu à partir des utilisateurs réels plutôt que d'afficher son UUID.
- Les sidebars utilisent le signal `AuthService.utilisateur` et le profil est rafraîchi depuis `/api/auth/profil/`.
- Les données métier fictives repérées (retard chiffré arbitraire, noms, montants, anomalies) ne sont plus utilisées pour représenter l'état du projet.

## Backend attendu
Le front est aligné sur `http://127.0.0.1:8000/api` et attend notamment :
- `/auth/connexion/`, `/auth/profil/`
- `/utilisateurs/`
- `/projets/`, `/etapes/`, `/avancements/`
- `/depenses/`
- `/justificatifs/`, `/extractions-ocr/`, `/documents/`
- `/analyses/`, `/anomalies/`, `/recommandations/`
- `/demandes/`, `/alertes/`, `/historique/`

## Validation
Une inspection statique a été faite sur les bindings et appels API. L'environnement d'exécution fourni ici n'a pas réussi à terminer `npm install` dans la limite disponible, donc le build Angular réel doit encore être exécuté localement avec `npm install && ng build`.
