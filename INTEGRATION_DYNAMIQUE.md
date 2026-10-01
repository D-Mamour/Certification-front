# Chantial — Front dynamique

Les données métier fictives ont été retirées des composants principaux.
Les écrans utilisent désormais l'API Django : projets, étapes, avancements,
dépenses, justificatifs, analyses, anomalies, recommandations, alertes,
demandes, historique et utilisateurs.

Le HTML/CSS et la structure visuelle d'origine sont conservés. Les changements
HTML se limitent aux bindings Angular nécessaires pour remplacer les valeurs
fictives par les valeurs reçues de l'API.

Un backend compagnon est fourni car le backend d'origine ne possédait pas
d'endpoint REST administrateur `/api/utilisateurs/`, indispensable pour rendre
l'écran Administrateur réellement dynamique.
