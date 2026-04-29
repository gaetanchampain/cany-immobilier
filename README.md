# Cany Immobilier — Maquette de site web

Maquette éditoriale pour **Cany Immobilier**, agence du Pays de Caux spécialisée dans la transmission de manoirs, châteaux et maisons de maître entre Étretat et la Côte d'Albâtre.

🌐 **Démo en ligne :** [https://VOTRE-NOM-UTILISATEUR.github.io/cany-immobilier/](https://VOTRE-NOM-UTILISATEUR.github.io/cany-immobilier/)
> Remplacez `VOTRE-NOM-UTILISATEUR` par votre identifiant GitHub une fois le site publié.

---

## Aperçu

Site vitrine en trois pages, accessible via une navigation à hash routing (single-page application légère, sans framework) :

- **Accueil** (`#/`) — Manifeste, biens emblématiques, ancrage normand, équipe
- **Nos biens à vendre** (`#/biens`) — Catalogue filtrable (24 biens, 7 villages)
- **Fiche bien** (`#/bien-chantoiseau`) — Exemple de page détail (Manoir de Chantoiseau)

## Caractéristiques

- ✅ **Responsive** — Testé sur desktop (1440 px), laptop (1024 px), tablette (768 px), iPhone 13 (390 px) et iPhone SE (320 px)
- ✅ **Menu burger mobile** avec drawer plein écran et croix de fermeture
- ✅ **Aucun framework** — HTML / CSS / JavaScript vanilla, pas de dépendance npm
- ✅ **Typographie soignée** — Fraunces (serif éditorial) + Inter (sans-serif), polices auto-hébergées
- ✅ **21 photos** intégrées localement (libres de droits via [Unsplash](https://unsplash.com))
- ✅ **Léger** — 2,9 Mo total (HTML + CSS + 13 fonts + 21 images)

## Structure du projet

```
cany-immobilier/
├── index.html              ← page unique (les 3 routes y cohabitent)
├── assets/
│   ├── styles.css          ← tous les styles (~3 300 lignes)
│   ├── fonts/              ← 13 fichiers woff2 (Fraunces + Inter, sous-ensembles latin)
│   └── images/             ← 21 photos JPEG
└── README.md
```

## Lancer en local

```bash
# Cloner le dépôt
git clone https://github.com/VOTRE-NOM-UTILISATEUR/cany-immobilier.git
cd cany-immobilier

# Servir avec n'importe quel serveur HTTP statique
python3 -m http.server 8000
# ou
npx serve .

# Puis ouvrir http://localhost:8000
```

> ⚠️ Ne pas ouvrir `index.html` directement avec `file://` : les hash routes (`#/biens`) fonctionnent, mais certaines fonctionnalités (preconnect, sécurité des navigateurs) demandent un vrai serveur HTTP.

## Charte graphique

| Couleur | Hex | Usage |
|---|---|---|
| Noir profond | `#14110E` | Fond principal |
| Lin chaud | `#EFE6D2` | Texte sur fond noir |
| Brique | `#C45430` | CTA, accents |
| Brique chaude | `#D87358` | Italiques d'accent |

**Polices :** [Fraunces](https://fonts.google.com/specimen/Fraunces) (serif éditorial moderne) + [Inter](https://fonts.google.com/specimen/Inter) (sans-serif technique).

## Notes pour l'agence

- Toutes les **photos sont des placeholders** issues d'Unsplash — à remplacer par les biens réels de Cany Immobilier
- Les **textes sont des exemples** (Château de B***, Manoir de Chantoiseau, etc.) — à adapter au catalogue réel
- Les **coordonnées** (`02 35 97 12 34`, `contact@cany-immobilier.fr`) sont indicatives
- Le **système de filtres** sur la page biens fonctionne visuellement mais n'est pas connecté à un CMS
- La **bascule FR / EN** est présente mais non fonctionnelle (à connecter à une logique de traduction si retenue)

## Évolutions possibles

Si la maquette est validée, voici les chantiers naturels d'industrialisation :

1. **CMS headless** (Strapi, Sanity, Contentful) pour que l'agence saisisse les biens elle-même
2. **Conversion en multi-pages statiques** (Astro, Eleventy) pour un meilleur référencement Google
3. **Optimisation images** (formats WebP / AVIF, dimensions multiples avec `srcset`)
4. **Formulaire de contact** branché sur un service (Formspree, Web3Forms, ou backend dédié)
5. **Espace agent** avec authentification pour gestion des biens

---

**Conception et développement** — Maquette réalisée à titre de démonstration.
