# Sécurité frontend — Chantial

Le frontend applique : validation des e-mails, longueur maximale, messages d'authentification génériques, JWT limité à `sessionStorage`, ajout automatique du Bearer token, renouvellement centralisé, `noopener,noreferrer` sur les ouvertures de documents, et formulaires Angular réactifs.

## À imposer côté Django avant production

Le frontend ne peut pas assurer seul la sécurité d'authentification. En production : HTTPS obligatoire ; CORS limité au domaine Angular ; `DEBUG=False` ; `ALLOWED_HOSTS` explicite ; mot de passe validé par les validateurs Django ; limitation des tentatives de connexion ; permissions DRF vérifiées serveur ; validation/normalisation d'e-mail serveur ; taille/type des fichiers contrôlés serveur ; secrets uniquement dans `.env` ; et, idéalement, JWT déplacés vers des cookies `HttpOnly`, `Secure`, `SameSite` avec stratégie CSRF adaptée.


## Recommandations backend indispensables avant production

Le frontend ne peut pas imposer ces protections. Elles doivent être configurées dans Django :

- placer idéalement le **refresh token** dans un cookie `HttpOnly`, `Secure` et `SameSite`;
- conserver les contrôles de rôle et de propriété sur chaque endpoint (le masquage Angular n'est pas une autorisation);
- limiter les tentatives de connexion et de réinitialisation de mot de passe;
- normaliser les adresses e-mail côté serveur et imposer leur unicité;
- ne jamais révéler si une adresse e-mail existe dans les messages d'authentification;
- valider le type, la taille et le contenu des fichiers justificatifs côté serveur;
- utiliser HTTPS en production et une configuration CORS/CSRF restrictive;
- conserver une trace des décisions sensibles dans l'audit.

Dans cette V1, `sessionStorage` limite la persistance des JWT à l'onglet mais **ne protège pas contre une XSS**. La migration vers un refresh token HttpOnly doit être faite conjointement avec le backend afin de ne pas casser le mécanisme actuel de rafraîchissement.
