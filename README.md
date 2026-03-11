# עברית — Programme Intensif

Application web d'apprentissage de l'hébreu — 1h/jour × 5 jours/semaine. Niveau A2+/B1.

**Fichier unique, zéro dépendance, fonctionne offline.**

---

## Déploiement

### GitHub Pages (recommandé — gratuit)

1. Crée un repo GitHub (ex: `hebrew-programme`)
2. Upload `index.html` à la racine
3. Settings → Pages → Source : `main` branch, `/ (root)`
4. Accessible sur `https://[ton-username].github.io/hebrew-programme`

### Netlify Drop

1. Va sur [app.netlify.com/drop](https://app.netlify.com/drop)
2. Glisse-dépose le fichier `index.html`
3. URL générée instantanément

### En local

```bash
# Ouvre simplement le fichier dans ton navigateur
open index.html

# Ou avec un serveur local (si tu veux tester localStorage)
npx serve .
# ou
python3 -m http.server 8080
```

### ⚠️ Pourquoi ça ne marche pas sur Vercel

Vercel s'attend à un framework (Next.js, Vite, etc.) ou une structure de projet. Pour un fichier HTML statique seul, il faut soit :
- Ajouter un fichier `vercel.json` à la racine :

```json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }]
}
```

- Ou utiliser GitHub Pages / Netlify Drop qui acceptent nativement les fichiers HTML statiques.

---

## Structure

```
.
└── index.html          # Application complète (auto-contenu)
```

Tout est dans un seul fichier HTML — CSS, JS, contenu pédagogique. Aucune dépendance externe sauf Google Fonts.

---

## Contenu pédagogique

### 5 sessions × 6 exercices (~60 min chacune)

| Jour | Thème | Grammaire |
|------|-------|-----------|
| 1 | Temps & négation | Binyan Pa'al — Passé |
| 2 | Commerce & négociation | Binyan Pi'el — Présent |
| 3 | Futur & projets | Futur Pa'al |
| 4 | Vie quotidienne Tel Aviv | Binyan Hif'il |
| 5 | Révision & consolidation | Quiz mixte |

### Exercices par session

- **Flashcards** — 10 mots avec exemple contextuel, auto-évaluation honnête
- **Conjugaison** — tableau complet + mini-quiz 4 questions
- **Blancs à compléter** — 5 phrases en contexte hébreu
- **Lecture** — texte en hébreu, tooltip sur chaque mot au survol
- **Traduction** — FR→HEB ou HEB→FR selon le jour
- **Récapitulatif** — score par exercice, mots du jour

### Statistiques hebdomadaires

- Score par session (graphique barres)
- Performance par compétence (vocabulaire / conjugaison / lecture / traduction)
- Mots maîtrisés vs mots à retravailler
- Persistance via `localStorage` (données conservées entre sessions)

---

## Personnalisation

Le contenu est dans des objets JS au début du `<script>` :

```
VOCAB         — mots par jour (10 mots × 5 jours)
CONJUGATION_DATA — tableaux de conjugaison + quiz
FILL_DATA     — phrases à compléter
READING_DATA  — textes de lecture + questions
TRANSLATION_DATA — paires de traduction
```

Pour modifier le contenu, édite directement ces objets dans `index.html`.

---

## Données

Les données sont stockées dans `localStorage` sous la clé `heb_state_v2`. Elles se réinitialisent automatiquement chaque semaine (basé sur le numéro de semaine ISO).

Pour réinitialiser manuellement :

```javascript
localStorage.removeItem('heb_state_v2')
```

---

## Niveau cible

A2+/B1 — correspond à environ 150-200h d'hébreu. Les exercices couvrent :
- Les binyanim Pa'al, Pi'el, Hif'il (passé, présent, futur)
- Vocabulaire professionnel et quotidien (Tel Aviv)
- Compréhension écrite de textes courts
- Production écrite guidée
