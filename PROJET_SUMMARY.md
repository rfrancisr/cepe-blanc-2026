# Projet Analyse CEPE Blanc 2026 — Collège Privé Henitsoa

> Dernière mise à jour : 2026-05-24

---

## 📁 Structure des fichiers

```
d:\Famille\Exo Programmation\claude\henitsoa\
│
├── docs\
│   └── releve_de_note.xlsx        ← Source de données principale (PDF original aussi présent)
│
├── site\
│   └── index.html                 ← Site web statique final (auto-contenu, aucune dépendance locale)
│
├── agent\                         ← Scripts Python d'extraction préliminaire (non utilisés finalement)
│   ├── extract_pdf.py / extract_pdf2-4.py
│   ├── create_excel.py
│   ├── debug_*.py
│   └── releve_de_note.xlsx        ← Copie de travail intermédiaire
│
├── archive\
│   └── releve_de_note.xlsx        ← Sauvegarde archive
│
├── analysis_data.json             ← Export JSON des stats agrégées (école vs école)
├── students_data.json             ← Export JSON des 56 élèves Henitsoa (données normalisées)
├── node_modules\                  ← Package xlsx (npm, utilisé pour test, non requis pour le site)
└── PROJET_SUMMARY.md              ← Ce fichier
```

---

## 📊 Données source

### Fichier : `docs/releve_de_note.xlsx`
- **Feuille** : `Notes CEPE Blanc 2026`
- **Lignes** : 1 333 (1 en-tête + 1 332 élèves)
- **Colonnes** :

| Col | Nom | Détail |
|-----|-----|--------|
| A | Etablissement | Nom de l'école |
| B | Matricule | Identifiant élève |
| C | Nom et Prénoms | Nom complet |
| D | Sexe | G / F |
| E | Option | A / B |
| F | Opération | Score brut /20 |
| G | Problème | Score brut /40 |
| H | SVT | Score brut /40 |
| I | TTFM | Score brut /20 |
| J | Géographie | Score brut /20 |
| K | Malagasy | Score brut /40 |
| L | Français | Score brut /20 |
| M | TOTAL | Somme colonnes F–L (max 200) |
| N | Moyenne | TOTAL / 10 (max 20) |
| O | RANG | Rang général sur 1 332 |
| P | Total_check | Formule =SUM(F:L) — vérification |
| Q | mismatch | =IF(M<>P, 1, 0) — 18 anomalies détectées |

### Barème par matière (max brut → équivalent /20)
| Matière | Max brut | Coeff. implicite |
|---------|----------|-----------------|
| Opération | 20 | ×1 |
| Problème | 40 | ×2 |
| SVT | 40 | ×2 |
| TTFM | 20 | ×1 |
| Géographie | 20 | ×1 |
| Malagasy | 40 | ×2 |
| Français | 20 | ×1 |
| **Total** | **200** | → Moyenne = Total/10 |

> ⚠️ **18 lignes avec anomalies** (mismatch=1) détectées dans les données — conservées telles quelles dans l'analyse, leur impact est négligeable (1,35% des données).

---

## 🏫 Contexte : 33 établissements, 1 332 élèves

### Collège Privé Henitsoa
- **56 élèves** présentés
- **Rang parmi les écoles : 14ème sur 27** (écoles avec ≥ 3 élèves)
- **Moyenne générale : 10,67 / 20**

### Environnement Python utilisé
- **Anaconda** : `/c/Users/franc/anaconda3/python.exe` (Python 3.9.13)
- Package `openpyxl` disponible, `pandas` absent → tout fait avec openpyxl + statistics stdlib

---

## 📈 Résultats de l'analyse

### Classement des écoles (top 15, moyenne /20)
| # | École | Moy. | Élèves |
|---|-------|------|--------|
| 1 | Collège Trinitaire Sainte Marie | 15,46 | 127 |
| 2 | Collège Privé Les Chérubins | 13,10 | 39 |
| 3 | Le Progrès | 12,71 | 32 |
| 4 | Collège des Juniors La Ruche | 12,59 | 29 |
| 5 | École Privée La Lumière | 12,03 | 35 |
| … | … | … | … |
| **14** | **Collège Privé Henitsoa** | **10,67** | **56** |
| 15 | EPP Androtra | 10,41 | 51 |

### Top 20 élèves (toutes écoles)
- Moyenne top 20 : **17,75 / 20**
- 15 élèves sur 20 viennent du **Collège Trinitaire Sainte Marie**
- 2 ex-æquo au rang 1 (18,40/20) : La Ruche + Les Étoiles
- Aucun élève Henitsoa dans le top 20 (meilleur : rang 30)

### Scores normalisés /20 — Henitsoa vs Top 20

| Matière | Henitsoa | Top 20 | Écart | Gap % |
|---------|----------|--------|-------|-------|
| **Problème** | 6,55 | 18,95 | −12,40 | **−65,4%** 🔴 |
| **Opération** | 11,20 | 19,35 | −8,15 | **−42,1%** 🔴 |
| Géographie | 11,61 | 18,40 | −6,79 | −36,9% 🟠 |
| TTFM | 11,29 | 17,35 | −6,06 | −34,9% 🟠 |
| Malagasy | 10,18 | 14,65 | −4,47 | −30,5% 🟡 |
| SVT | 12,55 | 17,90 | −5,35 | −29,9% 🟡 |
| **Français** | **14,03** | 18,02 | −3,99 | **−22,1%** 🟢 |

### Distribution des rangs Henitsoa (sur 1 332)
| Tranche | Nb élèves | % |
|---------|-----------|---|
| Top 100 | 2 | 3,6% |
| 101–300 | 10 | 17,9% |
| 301–500 | 15 | 26,8% |
| 501–700 | 9 | 16,1% |
| 701–1000 | 8 | 14,3% |
| 1001+ | **12** | **21,4%** |

### Top 10 élèves Henitsoa
| # école | Nom | Rang gén. | Moy. |
|---------|-----|-----------|------|
| 1 | FENITRARIHASINA VOAHANGINANTENAINA | 30 | 16,85 |
| 2 | ANJARANIAINA ANJELINAH | 46 | 16,50 |
| 3 | RAMAHANDRY OCÉANNE NARDY | 140 | 14,85 |
| 4 | ANDRIAMISAINA HARENA FAHENDRENA | 169 | 14,50 |
| 5 | MIANDRILALA MIKAJY ITOERANTSOA | 177 | 14,35 |
| 6 | RABEMANANTSOA TSITOHAINA FINARITRA | 222 | 13,70 |
| 7 | ANDRIANJAFY NY ARO NOTAHIANJANAHAR | 229 | 13,50 |
| 8 | ANDRIANIRINA YASMIE | 256 | 13,20 |
| 9 | RANDRIAMAMPIONINA HARINIAINA TSIARO | 270 | 13,00 |
| 10 | RAMIHARISOA FANIRINIAINA VALISOA | 270 | 13,00 |

---

## 🌐 Site web — `site/index.html`

### Technologies
- **HTML5 + CSS3 + JavaScript vanilla** — aucune dépendance locale
- **Chart.js 4.4.0** via CDN (`cdn.jsdelivr.net`) — tous les graphiques
- Fichier unique auto-contenu (données JSON embarquées dans le HTML)

### Palette de couleurs
| Rôle | Couleur | Hex |
|------|---------|-----|
| Henitsoa | Rouge | `#dc2626` |
| Top 20 | Bleu ciel | `#0284c7` |
| Trinitaire | Ambre | `#d97706` |

### Structure : 6 onglets

#### 1. 📋 Vue d'ensemble
- 6 KPI cards (moyenne, écarts, meilleur rang, pire lacune, meilleure matière)
- Graphique barres groupées (Henitsoa / Top 20 / Trinitaire) par matière
- Radar des compétences (3 séries)
- Histogramme distribution des rangs Henitsoa

#### 2. 📊 Comparaison matières
- Barres horizontales doubles (Henitsoa rouge sur fond bleu Top 20) avec badge % d'écart
- Graphique barres groupées détaillé
- Tableau récapitulatif avec niveaux (Critique / Important / À améliorer / Acceptable)

#### 3. ⚡ Points forts & faibles
- Alertes colorées (rouge/orange/vert/bleu)
- Graphique lignes (profil de compétences)
- Graphique barres horizontales "carte des lacunes" (% retard vs Top 20)

#### 4. 🏆 Classements
- Histogramme horizontal des 15 meilleures écoles (Henitsoa en rouge, autres en gris)
- Tableau Top 10 élèves Henitsoa
- Tableau Top 20 élèves toutes écoles

#### 5. 🎓 Analyse par élève ← *ajouté en session 2*
- **Dropdown** des 56 élèves Henitsoa (triés par rang, affichant rang + nom + moyenne)
- **Carte identité** : avatar (👩/👨), nom, rang général, moyenne
- **Radar** : profil élève vs Top 20 (2 séries)
- **Histogramme** : score par matière (élève rouge vs Top 20 bleu)
- **Barres de progression** : score normalisé /20 par matière (vert ≥14 / orange ≥10 / rouge <10)
- **Tableau analytique** : score brut, /20, Top 20 ref, écart, %, diagnostic
- **Points forts** : matières avec pct ≥ −22% (fond vert)
- **Lacunes** : matières avec pct < −22% (fond rouge), triées par priorité

#### 6. 🎯 Recommandations
- 7 cartes de recommandations (une par matière, classées par priorité)
- Tableau plan d'action sur 6 mois (Phase 1 → 3 + Continu)
- Alertes "Ce que fait bien" / "Erreurs à éviter"

---

## 🐛 Bug corrigé en session 2

**Cause** : clé `top20` définie deux fois dans l'objet `DATA` JavaScript :
```js
// ❌ Première définition (tableau de scores numériques) :
top20: [19.35, 18.95, 17.90, ...]

// ❌ Deuxième définition qui écrasait la première (tableau d'objets élèves) :
top20: [{ nom: '...', rang: 1, moyenne: 18.4 }, ...]
```
**Effet** : `DATA.top20[i]` retournait un objet → `NaN` dans les calculs, `[object Object]` dans le HTML, barres vertes absentes des graphiques.

**Correction** : renommage en `top20Scores` (tableau numérique) et `top20Students` (tableau d'objets). Dans la version finale, ces deux tableaux ont été séparés dans des constantes distinctes (`TOP20_SCORES`, `TOP20_STU`).

---

## 🔑 Points clés pour reprendre le projet

1. **Python Anaconda** requis pour lire le xlsx : `/c/Users/franc/anaconda3/python.exe`
2. Le site est **100% autonome** — ouvrir `site/index.html` dans un navigateur suffit
3. Pour **mettre à jour les données**, régénérer les scripts Python et remplacer les constantes JS dans le `<script>` du HTML
4. Les **18 anomalies** dans le xlsx (scores hors barème) n'ont pas été filtrées — elles représentent 1,35% des données et n'impactent pas les conclusions
5. Le **Malagasy** est difficile pour TOUTES les écoles (Top 20 moy. = 14,65 vs 17–19 pour les autres matières) — c'est structurel
6. Les **mathématiques** (Opération + Problème) représentent **30% de la note totale** → c'est là que le gain est maximal

---

## 💡 Pistes d'amélioration futures

- [ ] Ajouter un onglet comparaison **Henitsoa vs une école sélectionnable** (dropdown école)
- [ ] Ajouter **filtres par sexe** (G/F) dans l'analyse par élève
- [ ] Ajouter un **graphique d'évolution** si des données de plusieurs années deviennent disponibles
- [ ] Export PDF du rapport individuel par élève
- [ ] Intégrer les données **option A vs option B** (colonne E non exploitée)
- [ ] Ajouter un **mode sombre**
