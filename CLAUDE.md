# CLAUDE.md — Collège Privé Henitsoa · Analyse CEPE Blanc 2026

> Fichier de contexte pour Claude Code. Lire en priorité avant toute modification du projet.

---

## Vue d'ensemble

Analyse comparative des résultats d'examen blanc CEPE 2026 pour le **Collège Privé Henitsoa**.
Livrable : un **site web statique** (`site/index.html`) avec graphiques et analyse par élève.

---

## Fichiers importants

| Fichier | Rôle |
|---------|------|
| `docs/releve_de_note.xlsx` | Source de données principale (ne pas modifier) |
| `site/index.html` | Livrable final — ouvrir directement dans le navigateur |
| `PROJET_SUMMARY.md` | Documentation complète (structure, données, bugs, architecture) |

---

## Données

- **1 332 élèves** · **33 établissements** · **7 matières**
- **56 élèves Henitsoa** · rang **14ème/27** · moyenne **10,67/20**
- Barème : Opération /20 · Problème /40 · SVT /40 · TTFM /20 · Géographie /20 · Malagasy /40 · Français /20 → Total /200 → Moyenne = Total/10

## Résultats clés

| Matière | Henitsoa | Top 20 | Gap |
|---------|----------|--------|-----|
| Problème | 6,55/20 | 18,95/20 | **−65%** 🔴 |
| Opération | 11,20/20 | 19,35/20 | **−42%** 🔴 |
| Français | 14,03/20 | 18,02/20 | −22% 🟢 |

---

## Environnement technique

- **Python** : Anaconda → `/c/Users/franc/anaconda3/python.exe` (Python 3.9.13)
- Packages disponibles : `openpyxl` ✅ · `pandas` ❌
- **Node.js** : v22.11.0 (disponible si besoin)
- **Shell** : Git Bash (préféré) — PowerShell aussi disponible

---

## Architecture du site (`site/index.html`)

- Fichier HTML unique, **autonome** (données JSON embarquées)
- **Chart.js 4.4.0** via CDN — aucune dépendance locale
- **6 onglets** : Vue d'ensemble · Comparaison matières · Points forts/faibles · Classements · Analyse par élève · Recommandations
- Palette : Henitsoa `#dc2626` (rouge) · Top 20 `#0284c7` (bleu) · Trinitaire `#d97706` (ambre)

### Constantes JS clés dans `site/index.html`

```js
HEN_SCORES   = [11.20, 6.55, 12.55, 11.29, 11.61, 10.18, 14.03]  // scores normalisés /20
TOP20_SCORES = [19.35, 18.95, 17.90, 17.35, 18.40, 14.65, 18.02]
TRI_SCORES   = [18.28, 18.03, 15.59, 15.39, 15.30, 11.74, 14.98]
STUDENTS     // objet JSON avec les 56 élèves Henitsoa (norm, raw, gaps, pcts)
```

---

## Bug corrigé (à ne pas réintroduire)

Clé `top20` définie deux fois dans l'objet `DATA` → la liste d'élèves écrasait le tableau de scores.
**Fix** : constantes séparées `TOP20_SCORES` (nombres) et `TOP20_STU` (objets élèves).

---

## Pistes d'amélioration futures

- [ ] Onglet comparaison Henitsoa vs école sélectionnable (dropdown)
- [ ] Filtre par sexe (G/F) dans l'analyse par élève
- [ ] Export PDF du rapport individuel par élève
- [ ] Exploiter la colonne Option (A/B) non encore analysée
- [ ] Graphique d'évolution si données multi-années disponibles
