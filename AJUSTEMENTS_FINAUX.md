# Ajustements finaux du frontend

- Ma construction (bailleur) : projet chargé en premier ; une erreur d'API secondaire ne masque plus la construction.
- États de chargement, erreur et absence de projet rendus explicites.
- OCR : complétude des champs, champs manquants et texte OCR brut visibles ; aucune fausse valeur de confiance.
- Dashboard bailleur : indice de suivi et cohérence coût/avancement calculés à partir des données réelles.
- Typographie : une seule famille globale (Inter / system sans-serif), y compris boutons, champs et titres `.font-display`.
- Aucune donnée métier fictive ajoutée.

À valider localement : `npm install` puis `ng build` (installation npm indisponible dans l'environnement de génération).
