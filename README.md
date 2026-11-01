# MARKET DZ

Logiciel de gestion pour épiceries, mini-markets et supérettes : tableau de bord, caisse, historique des ventes, produits, stock. Français et arabe, PC / tablette / téléphone.

## Contenu du projet

- `index.html` : toute l’application (HTML, CSS et JavaScript dans un seul fichier, aucune installation requise)
- `vercel.json` : réglages d’hébergement Vercel
- `README.md` : ce guide

## Tester sur votre ordinateur

Double-cliquez sur `index.html` : il s’ouvre dans votre navigateur. (Une connexion Internet sert seulement à charger les polices.)

## Mettre en ligne sur Vercel (méthode GitHub, recommandée)

1. Créez un compte gratuit sur github.com et un nouveau dépôt, par exemple `market-dz`.
2. Dans le dépôt, cliquez sur « Add file » puis « Upload files » et déposez les fichiers du dossier (dézippé). Validez avec « Commit changes ».
3. Créez un compte sur vercel.com (connexion avec GitHub), puis « Add New… » > « Project » et importez le dépôt `market-dz`.
4. Laissez les réglages par défaut (Framework : « Other », aucune commande de build), puis cliquez sur « Deploy ».
5. Vercel vous donne un lien du type `market-dz.vercel.app`. Chaque modification envoyée sur GitHub met le site à jour.

## Autre méthode : ligne de commande

Avec Node.js installé, dans le dossier du projet :

    npx vercel        # première mise en ligne (test)
    npx vercel --prod # mise en ligne définitive

## Votre propre nom de domaine

Dans Vercel : Project > Settings > Domains, ajoutez votre domaine et suivez les instructions DNS.

## Important : où sont les données

- Les produits, ventes et mouvements de stock sont enregistrés dans le navigateur de chaque appareil (localStorage, clé `marketdz.v1`). **Ce n’est pas une base de données.**
- Chaque commerçant garde donc ses données sur son appareil et son navigateur, séparées de celles des autres clients. Rien n’est partagé entre appareils.
- Vider les données du navigateur efface tout. Les données saisies dans la version de démonstration Claude ne sont pas transférées vers votre nouveau lien.
- Pour plusieurs appareils, sauvegardes et comptes utilisateurs, il faut la migration décrite ci-dessous.

## Préparation de la migration Supabase / PostgreSQL

Tout l’accès au stockage passe par l’objet `Store` (fonctions `load` et `save`) dans `index.html`. La migration consiste à le remplacer par un adaptateur Supabase, avec des tables filtrées par `shop_id` :
`shops`, `products`, `sales`, `sale_items`, `stock_moves`, plus des comptes utilisateurs (Supabase Auth) et des règles d’accès (Row Level Security) pour que chaque commerce ne voie que ses données.

## Fonctions disponibles / à venir

Disponibles : caisse (panier, paiements, ticket, impression, PDF), historique des ventes, produits (ajout, modification, suppression, recherche), stock (entrées, sorties, alertes), tableau de bord (chiffre d’affaires, bénéfice estimé, marge, graphiques, meilleurs produits).
À venir : import Excel, photos de produits, dates de péremption, sauvegarde/export des données, multi-appareils.
