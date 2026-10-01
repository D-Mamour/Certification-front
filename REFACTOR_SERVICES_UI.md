# Refactorisation Chantial Front

- `chantial-api.service.ts` supprimé.
- Six services conservés : Auth, Projet, Finance, Document, Intelligence, Interaction.
- Les composants utilisent le service correspondant à leur domaine.
- Aucune donnée métier statique n'a été réintroduite.
- Les interfaces et leur structure ont été conservées.
- Harmonisation visuelle : Inter/system-ui, texte principal #0F172A, texte secondaire #64748B,
  accent #0284C7, fond #F8FAFC, bordures #E2E8F0. Les couleurs sémantiques
  (succès, alerte, anomalie) restent dédiées à leur signification.
- L'installation npm/build n'a pas pu être terminée dans l'environnement d'exécution ;
  exécuter `npm install` puis `npm run build` localement pour la validation Angular finale.
