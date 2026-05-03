# 📊 SenWebStats 🇸🇳
## Statistiques & Performances des Sites Web Sénégalais

> L'équivalent sénégalais de Semrush/Ahrefs — 100% sources gratuites.

---

## 🎯 Objectif

Analyser et comparer les performances web des sites sénégalais (presse, e-commerce, téléphonie, banque, emploi) en collectant :

- **Métadonnées HTML** : title, description, structure, liens
- **Performance** : Google PageSpeed (Core Web Vitals)
- **Backlinks** : CommonCrawl Index (gratuit)
- **Estimation de trafic** : Modèle CTR × Volume de recherche

---

## 🚀 Installation

```bash
# 1. Cloner / créer le projet
cd senwebstats

# 2. Installer les dépendances
pip install -r requirements.txt

# 3. Initialiser la base de données
python main.py init

# 4. Lancer la collecte
python main.py crawl          # Métadonnées HTML
python main.py perf           # Performance PageSpeed
python main.py backlinks      # Backlinks CommonCrawl

# 5. Lancer l'app Streamlit
streamlit run app/streamlit_app.py
```

---

## 📁 Structure du Projet

```
AS3_webscrapping_2026/
├── main.py                  # Point d'entrée CLI
├── metadata_scraper.py      # Scraper HTML principal
├── pagespeed_collector.py   # Google PageSpeed API
├── backlinks_collector.py   # Backlinks CommonCrawl
├── scoring_model.py         # Modèle de scoring & estimation trafic
├── streamlit_app.py         # Dashboard Streamlit
├── schema.py                # Schéma SQLite + fonctions DB
├── sites.py                 # Liste des sites cibles + config
├── setup_project.py         # Initialisation du projet
├── .streamlit/              # Configuration thème Streamlit
└── requirements.txt
```


---

## 🔧 Commandes Disponibles

| Commande | Description |
|---|---|
| `python main.py init` | Initialiser DB + insérer les sites |
| `python main.py crawl` | Crawler tous les sites |
| `python main.py crawl --cat presse` | Crawler une catégorie spécifique |
| `python main.py perf` | Collecter les scores PageSpeed (mobile) |
| `python main.py perf --strategy desktop` | Scores PageSpeed en mode desktop |
| `python main.py backlinks` | Collecter les backlinks CommonCrawl |
| `python main.py full` | Tout collecter en une seule commande |
| `python main.py report` | Rapport synthétique en terminal |
| `python scoring_model.py` | Calculer les scores & estimer le trafic |
| `streamlit run streamlit_app.py` | Lancer le dashboard interactif |

---

## 📊 Métriques Collectées

### Métadonnées HTML (`metadata_scraper.py`)
- Title, meta description, meta keywords
- Balises Open Graph (og:title, og:description, og:image)
- Canonical URL, robots meta
- Comptage H1 / H2
- Liens internes / externes
- Images totales et images avec attribut `alt`
- Nombre de mots dans la page
- SSL, Sitemap, Robots.txt
- Code HTTP et temps de réponse (ms)

### Performance (`pagespeed_collector.py`)
- Scores Performance, SEO, Accessibilité, Bonnes Pratiques (0–100)
- LCP · FCP · TTFB · CLS · TTI

### Backlinks (`backlinks_collector.py`)
- Total pages indexées
- Nombre de domaines référents
- Top domaines référents
- Évolution vs collecte précédente

---

## 🧮 Modèle de Scoring (`scoring_model.py`)

Le cœur du projet : un modèle propriétaire qui calcule 4 scores pour chaque site
à partir des données collectées, sans recourir à des API payantes.

| Score | Composition | Poids dans le score global |
|---|---|---|
| **Autorité** | Backlinks (60%) + Domaines référents (40%) | 45% |
| **Qualité** | SEO (40%) + Performance (35%) + Accessibilité (25%) | 35% |
| **Technique** | Vitesse (40%) + SSL (20%) + Sitemap (15%) + Contenu (25%) | 20% |
| **Global** | Moyenne pondérée des 3 scores | — |

**Estimation du trafic mensuel** — loi de puissance par catégorie :

trafic_estimé = base_catégorie × (score_global / 100) ^ 1.5

> L'exposant 1.5 modélise la domination des meilleurs sites, conformément
> à la loi de puissance observée sur le web (effet "winner-takes-most").

Bases calibrées sur SimilarWeb Africa 2024 :

| Catégorie | Base mensuelle |
|---|---|
| Presse | 250 000 visites |
| Téléphonie | 120 000 visites |
| E-commerce | 80 000 visites |
| Banque/Finance | 60 000 visites |
| Emploi | 40 000 visites |

---

## 🗂️ Sites Suivis

| Catégorie | Sites |
|---|---|
| 📰 Presse | Seneweb, Dakaractu, Senenews, Rewmi, Leral, Senego... |
| 🛒 E-commerce | Jumia SN, Expat Dakar, CoinAfrique, Afrikrea... |
| 📱 Téléphonie | Orange SN, Free SN, Expresso, Sonatel |
| 🏦 Banque/Finance | CBAO, Ecobank SN, Wave, Orange Money |
| 💼 Emploi | Senjob, Emploi.sn, Rekrute SN |

---

## ⚠️ Bonnes Pratiques Respectées

- Délais aléatoires entre requêtes (2–5 secondes)
- Rotation des User-Agents
- Respect des fichiers `robots.txt`
- API PageSpeed : gratuite jusqu'à 25 000 req/jour
- CommonCrawl : API Index uniquement (pas de téléchargement massif)

---

## 🗺️ Roadmap élaboré

- [ ] Scraper métadonnées HTML
- [ ] Collecte Google PageSpeed (Core Web Vitals)
- [ ] Backlinks CommonCrawl
- [ ] Base de données SQLite structurée
- [ ] Dashboard Streamlit interactif
- [ ] Modèle de scoring multi-critères
- [ ] Estimation de trafic (loi de puissance)
- [ ] Modèle CTR × Volume de recherche réel
- [ ] Scraping positions SERP Google
- [ ] Analyse de tendances temporelles
- [ ] Scheduler automatique (collecte quotidienne)
- [ ] API FastAPI publique
- [ ] Export CSV/Excel depuis le dashboard

---

## 👩‍💻 Auteurs

Projet réalisé dans le cadre du cours **AS3 — Webscraping**
Promotion 2025-2026




