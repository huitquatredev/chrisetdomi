# Caveau Chris & Domi — démo

Maquette haut de gamme pour **Le Caveau de Chris et Domi**, caviste familial à Orange (Vaucluse).  
Site statique construit avec **Astro**, pensé pour un hébergement **Vercel**.

## Lancer le projet

```bash
npm install
npm run dev       # http://localhost:4321
npm run build     # génère /dist
npm run preview   # prévisualise le build
```

## Pages

- `/` — page d’accueil (hero, maison, sélection, univers, tireuses, avis, accès).
- `/catalogue` — catalogue filtrable par univers, avec recherche.
- `/catalogue/[slug]` — fiche produit générée depuis les données.
- `/404` — page d’erreur.

Aucun panier, aucun paiement. Les fiches renvoient vers le téléphone de la boutique.

## Structure

```
src/
  components/      Header, Footer, ProductCard
  data/products.ts Catalogue + catégories + helpers prix
  layouts/         BaseLayout (SEO, JSON-LD, scripts globaux)
  pages/           index, catalogue, fiches produit, 404
  assets/          Photos d’ambiance (optimisées par Astro)
  styles/          Tokens, typographie, composants globaux
public/
  brand/           Logo source, versions transparentes, favicon
  catalogue/       Photos produits
  images/          Visuels des univers + image Open Graph
```

## Direction artistique

- Palette reprise du logo : bordeaux `#5c1a2b`, Rose `#d793ab`, crème `#f5f0e6`, encre `#241216`.
- **DM Serif Display** pour le registre éditorial (fonte choisie sur Beautiful Web Type, proche du logo mais plus chaleureuse que Bodoni), **Jost** pour les textes, les prix et les données pratiques.
- Photos plein cadre, arches, filets fins, beaucoup de respiration.
- Animations discrètes (révélation au scroll, survol des univers), désactivées avec `prefers-reduced-motion`.

## Contenu et sources

Les informations de la boutique sont réelles et publiques :

- 500 avenue de Verdun, lieu-dit Les Sables Ouest, 84100 Orange
- 04 88 84 86 67
- Caveau créé en 2012 par Christine et Dominique Gervasio, repris par leur fils Rémi
- Environ 2 500 références, 4,7/5 sur Google

Les références produits s’inspirent de [Vinatis](https://www.vinatis.com/) et de producteurs locaux :

- Appassimento Wrap Around, Jeff Carrel, Domaine de la Janasse, Domaine Hauvette, Domaine La Grange Tiphaine…
- Bau Blanc (Le Bau), Brasserie du Mont Ventoux, Brasserie Nepo
- Don Papa, Lagavulin, Citadelle, Martell, Henri Bardouin…

**À finaliser avant mise en ligne :** les prix sont indicatifs, l’adresse e-mail `contact@caveaudechrisetdomi.com` est un placeholder, et les visuels produits appartiennent à leurs marques respectives. La photo de Rémi en section « La maison » est le fichier `gervasio.jpg` fourni à la racine du projet (à valider pour les droits). Les autres photos d’ambiance viennent de Pexels (libres d’utilisation) ; les photos produits de Vinatis, Le Bau et Brasserie du Mont Ventoux sont utilisées ici à titre de démonstration uniquement.

## Personnalisation rapide

- **Produits, catégories, prix, notes de dégustation** : `src/data/products.ts`.
- **Coordonnées, horaires, textes** : `src/pages/index.astro` et `src/components/Footer.astro`.
- **Couleurs et typographie** : `src/styles/global.css`.
- **URL du site** : `astro.config.mjs` (`site`), `public/robots.txt` et `src/layouts/BaseLayout.astro`.
- **Logo** : `public/brand/logo-original.jpg` est la source ; `logo.png`, `logo-light.png`, `logo-mark.png` sont les déclinaisons utilisées.

## Déploiement Vercel

1. Pousser le dossier sur GitHub/GitLab.
2. Importer le dépôt dans Vercel.
3. Vercel détecte Astro : build `npm run build`, sortie `dist`.
4. Renseigner le domaine final, puis mettre à jour l’URL dans `astro.config.mjs` et `public/robots.txt`.

`vercel.json` force le framework Astro, les URL propres et l’absence de slash final.

## Vercel Web Analytics

Le projet inclut **`@vercel/analytics`**, avec le composant `<Analytics />` monté dans `src/layouts/BaseLayout.astro`.

Pour activer la collecte :

1. Ouvrir le projet dans Vercel.
2. Aller dans **Analytics** → **Enable**.
3. Redéployer le projet (le push sur `master` déclenche le déploiement).

Les statistiques apparaissent ensuite dans l’onglet **Analytics** du projet Vercel.  
En local, le script `/_vercel/insights/script.js` n’existe pas : c’est normal, la collecte ne fonctionne que sur un déploiement Vercel.

## Accessibilité & bonnes pratiques

- Structure sémantique, un seul `h1` par page, lien d’évitement.
- `alt` sur les images de contenu, `aria-hidden` sur les visuels décoratifs.
- Navigation clavier, focus visibles, menu mobile fermable avec `Échap`.
- `prefers-reduced-motion` respecté.
- JSON-LD `LiquorStore` sur tout le site et `Product` sur les fiches.
- Mention légale alcool présente dans le footer.
