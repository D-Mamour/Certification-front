# Corrections Angular TS2729

Les erreurs `Property 'auth' is used before its initialization` et `Property 'fb' is used before its initialization` venaient de champs de classe initialisés avant que les dépendances déclarées dans le constructeur ne soient disponibles avec la configuration TypeScript/Angular actuelle.

Correction appliquée :
- `AuthService` est injecté avec `inject(AuthService)` avant l'initialisation de `utilisateur` dans les composants concernés.
- `FormBuilder` est injecté avec `inject(FormBuilder)` avant la création des formulaires concernés.
- Les six services Angular sont commentés en français.
- `chantial-api.service.ts` reste supprimé.
- Les couleurs historiques restantes dans les fichiers TypeScript concernés ont été alignées sur la palette Chantial (`#0284C7`, etc.).

Composants corrigés :
- `Bailleur/dashboard-bailleur/dashboard-bailleur.ts`
- `Bailleur/demande/demande.ts`
- `Bailleur/orc-controle/orc-controle.ts`
- `Entrepreneur/ajout-depense/ajout-depense.ts`
- `Entrepreneur/analyse/analyse.ts`

Validation locale recommandée :

```bash
npm install
ng serve
```

Le build Angular n'a pas pu être exécuté dans l'environnement de génération, car les dépendances Angular locales n'y sont pas complètement installées.
