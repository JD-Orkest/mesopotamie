# TODO — Mésopotamie : Finalisation du site

Liste exhaustive des étapes manuelles à réaliser pour finaliser et déployer le site.

---

## 1. Installation & Configuration initiale

Le projet est déjà scaffoldé et GSAP est installé. Si vous clonez le dépôt :

```bash
cd mesopotamie
npm install
```

Démarrer le serveur de développement :
```bash
npm run dev
```

Construire pour la production :
```bash
npm run build
```

---

## 2. Polices Google Fonts (déjà configuré dans `index.html`)

✅ **Déjà fait** — Les polices sont chargées dans `index.html` via :
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&family=Playfair+Display:ital,wght@0,500;0,600;0,700;1,500&display=swap" rel="stylesheet" />
```

> **Optionnel pour la prod** : Téléchargez les polices en local (via [google-webfonts-helper](https://gwfh.mranftl.com/fonts)) et placez-les dans `public/fonts/` pour éviter la dépendance réseau.

---

## 3. Images à intégrer

### Emplacement des images
Placez toutes les images dans le dossier : **`/public/images/`**

### Liste des images requises

| Fichier attendu | Section | Description |
|---|---|---|
| `public/images/sumer.jpg` | Époques | Tablette cunéiforme sumérienne ou ziggurat d'Uruk |
| `public/images/akkad.jpg` | Époques | Buste de Sargon d'Akkad en bronze |
| `public/images/babylone.jpg` | Époques | Stèle d'Hammurabi ou représentation de Babylone |
| `public/images/tiamat-chaos.jpg` | Chaoskampf | Abstraction noire tourbillonnante (Tiamat) |
| `public/images/marduk-enuma.jpg` | Chaoskampf | Tablette de l'Enuma Elish ou bas-relief de Marduk |
| `public/images/transmission-1.jpg` | Transmission | Bas-relief babylonien du Mushkhushshu |
| `public/images/transmission-2.jpg` | Transmission | Scène chevalier médiéval vs dragon |
| `public/images/transmission-3.jpg` | Transmission | Tête de crocodile ou vitrine de musée |
| `public/images/ducasse-grand-place.jpg` | Rituels | Vue aérienne Grand-Place de Mons pendant la Ducasse |
| `public/images/moment-01.jpg` | Rituels | Collégiale Sainte-Waudru, châsse en procession |
| `public/images/moment-02.jpg` | Rituels | Car d'Or en procession |
| `public/images/moment-03.jpg` | Rituels | Foule poussant le Car d'Or dans la montée |
| `public/images/moment-04.jpg` | Rituels | Combat du Lumeçon sur la Grand-Place |
| `public/images/saint-georges.jpg` | Anatomie | Saint Georges en costume jaune et bleu |
| `public/images/dragon.jpg` | Anatomie | Dragon de la Ducasse |
| `public/images/chinchins.jpg` | Anatomie | Les Chinchins en costume rouge tartan |
| `public/images/hommes-feuilles.jpg` | Anatomie | Les Hommes de Feuilles |
| `public/images/diables.jpg` | Anatomie | Les Diables en salopette noire |
| `public/images/hommes-blancs.jpg` | Anatomie | Les Hommes Blancs |
| `public/images/dragon-gros-plan.jpg` | Anatomie | Gros plan tête du Dragon, gueule ouverte |

### Comment remplacer un placeholder

Dans chaque composant, cherchez le commentaire `<!-- PLACEHOLDER IMAGE -->` et remplacez :
```html
<!-- AVANT (placeholder) -->
<div class="img-placeholder" data-image-intent="..."></div>

<!-- APRÈS (image réelle) -->
<img src="/images/sumer.jpg" alt="Tablette cunéiforme sumérienne" />
```
> Le CSS `.img-placeholder img` gère déjà `object-fit: cover` et les dimensions.

---

## 4. Sources d'images recommandées

Pour des images libres de droits correspondant au sujet :

- **Artefacts mésopotamiens** :
  - [Wikimedia Commons](https://commons.wikimedia.org) — chercher "cuneiform tablet", "Sargon of Akkad", "Hammurabi stele", "Mushkhushshu"
  - [The British Museum Collection](https://www.britishmuseum.org/collection) — images haute résolution
  - [Louvre Collections](https://collections.louvre.fr) — nombreux artefacts mésopotamiens
  - [Rijksmuseum](https://www.rijksmuseum.nl/en/rijksstudio)

- **Ducasse de Mons** :
  - Site officiel : [www.mons.be/fr/doudou](https://www.mons.be/fr/doudou)
  - Contact la Ville de Mons pour les droits photographiques
  - [Visit Mons](https://www.visitmons.be)

- **Abstractions (Tiamat/chaos)** :
  - [Unsplash](https://unsplash.com) — chercher "dark marble texture", "black swirl abstract"
  - [Pexels](https://pexels.com) — "dark abstract fluid"

---

## 5. Personnalisation du contenu

### Textes
- Tous les textes sont directement dans les composants `.vue` dans les `data` ou dans le template.
- Pour modifier un texte, ouvrez le composant correspondant (`src/components/`) et éditez le contenu.

### Couleurs
Les couleurs sont des variables CSS dans `src/assets/styles/main.css` :
```css
--color-void:    #0F1115;   /* Fond principal */
--color-sand:    #E6DFD3;   /* Texte principal */
--color-lapis:   #004F98;   /* Accentuation (hover boutons) */
--color-gold:    #D4AF37;   /* Barre de progression, labels */
```

---

## 6. Optimisations recommandées avant mise en production

### Performance images
```bash
npm install --save-dev vite-plugin-imagemin
```
Ou utilisez un service CDN (Cloudinary, Imgix) pour les images avec transformation automatique.

### Métadonnées SEO
Dans `index.html`, mettez à jour :
- `<meta name="description" ...>` ✅ déjà fait
- Ajouter Open Graph tags :
```html
<meta property="og:title" content="MÉSOPOTAMIE — De l'ordre cosmique au folklore montois" />
<meta property="og:description" content="..." />
<meta property="og:image" content="/images/og-preview.jpg" />
<meta property="og:type" content="website" />
```

### Favicon
Remplacez `/public/vite.svg` par votre favicon (format `.ico` ou `.svg`).

---

## 7. Structure finale des fichiers

```
mesopotamie/
├── public/
│   ├── images/          ← Vos images vont ici
│   ├── fonts/           ← Optionnel (polices locales)
│   └── vite.svg         ← Remplacer par votre favicon
├── src/
│   ├── assets/
│   │   └── styles/
│   │       └── main.css ← Design System complet
│   ├── components/
│   │   ├── TheNavigation.vue
│   │   ├── HeroSection.vue
│   │   ├── EpoquesSection.vue
│   │   ├── ChaoskampfSection.vue
│   │   ├── TransmissionSection.vue
│   │   ├── RituelsSection.vue
│   │   ├── AnatomieSection.vue
│   │   └── TheFooter.vue
│   ├── App.vue
│   └── main.js
├── index.html            ← Polices Google Fonts incluses
├── package.json          ← GSAP déjà installé
├── vite.config.js
└── TODO.md               ← Ce fichier
```

---

## 8. Déploiement

### Vercel (recommandé)
```bash
npm install -g vercel
vercel
```

### Netlify
```bash
npm run build
# Déposer le dossier /dist sur app.netlify.com
```

### GitHub Pages
```bash
npm install --save-dev gh-pages
```
Ajouter dans `vite.config.js` :
```js
export default defineConfig({
  base: '/nom-du-repo/',
  plugins: [vue()],
})
```

---

## 9. Ajustements visuels suggérés

- [ ] Tester le rendu des animations GSAP sur mobile (ScrollTrigger peut nécessiter un `refresh()` après les images chargées)
- [ ] Ajouter un `loading="lazy"` sur toutes les balises `<img>` secondaires
- [ ] Tester le contraste des textes sur les images réelles (ajuster `--color-sand-dim`)
- [ ] Vérifier la performance du `backdrop-filter: blur` sur Safari iOS
- [ ] Optionnel : ajouter une page de chargement (`<Transition>`) pendant le chargement initial des polices

---

*Généré automatiquement — Projet Mésopotamie v1.0 — Mai 2026*
