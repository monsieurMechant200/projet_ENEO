# Projet AD2 #07 - Prévision de la Consommation Électrique au Cameroun (ENEO)

**École Nationale Supérieure Polytechnique de Douala**  
Département Informatique - Filière SDIA  
Année académique 2025/2026  
Enseignant : M. FOTSO Valdez

---

## Description

Ce projet a pour objectif de construire un pipeline complet d’analyse et de prévision de la consommation électrique à partir de **données synthétiques réalistes** construites sur des statistiques de l’Agence Internationale de l’Énergie (IEA).

La chaîne méthodologique suit les exigences de la Bible du projet **AD2 #07** et couvre :

1. **Analyse Exploratoire (EDA)** - visualisations multi‑échelles, boxplots, heatmaps  
2. **Prétraitement** - interpolation des valeurs manquantes, gestion des outliers (IQR), standardisation  
3. **ACP** – réduction dimensionnelle (95 % de variance expliquée)  
4. **Clustering** - K‑Means (k=4) pour le profilage des journées, DBSCAN pour la détection d’anomalies  
5. **Classification supervisée** - Arbre de décision & Random Forest pour identifier les heures critiques  
6. **Séries temporelles** - Décomposition saisonnière, test ADF, ACF/PACF, **SARIMA** avec prévision à 7 jours et intervalles de confiance 95 %  
7. **Rapport de risques de surcharge** – Recommandations opérationnelles pour ENEO  

L'ensemble du projet est consigné dans **un seul notebook Jupyter**, exécuté avec `random_state=42` pour garantir la reproductibilité.

---

## Structure du dépôt

```
projet07_consommation/
├── README.md
├── requirements.txt
├── .gitignore
├── projet07_ENEO_complet.ipynb          # Notebook Jupyter complet
├── images/                           # Graphiques générés par le notebook
│   ├── eda_multiscale.png
│   ├── eda_boxplot_heatmap.png
│   ├── eda_rolling_correlations.png
│   ├── preprocessing_outliers.png
│   ├── acp_scree_cercle.png
│   ├── acp_plan_factoriel.png
│   ├── kmeans_choix_k.png
│   ├── kmeans_profils.png
│   ├── dbscan_anomalies.png
│   ├── dt_confusion.png
│   ├── rf_importance_confusion.png
│   ├── series_temporelles_split.png
│   ├── decomposition_hebdomadaire.png
│   ├── decomposition_mensuelle.png
│   ├── acf_pacf.png
│   ├── sarima_diagnostics.png
│   ├── sarima_prevision_7j.png
│   └── rapport_risques_surcharge.png
├── eneo_presentation.html/           # Site vitrine interactif (dashboard)         
```

---

## Installation & utilisation

### 1. Cloner le dépôt
```bash
git clone <url-du-depot>
cd projet07_consommation
```

### 2. Créer un environnement virtuel (recommandé)
```bash
python -m venv venv
source venv/bin/activate     # Linux/Mac
venv\Scripts\activate        # Windows
```

### 3. Installer les dépendances
```bash
pip install -r requirements.txt
```

### 4. Lancer le notebook
```bash
jupyter notebook notebooks/projet07_final.ipynb
```

Exécutez toutes les cellules dans l’ordre (`Kernel → Restart & Run All`).

---

## Données

- **Source** : IEA Monthly Electricity Statistics (`MES_0126.csv`)  
- **Période** : janvier 2010 – janvier 2026  
- **Fréquence** : horaire (141 000 points)  
- Le jeu de données est **synthétique** et **rebaptisé « ENEO Cameroun »**, conformément à l’accord pédagogique (profil de charge africain, double pointe, saisonnalité adaptée).

---

## Méthodes & algorithmes

| Étape             | Technique / Modèle                              |
|-------------------|--------------------------------------------------|
| Réduction         | PCA (95 % variance)                              |
| Clustering        | K‑Means (k=4), DBSCAN (eps=0.5)                 |
| Classification    | Decision Tree, Random Forest (200 arbres)        |
| Séries temp.      | SARIMA(1,0,0)(1,0,0)[7] (auto_arima + statsmodels) |

---

## Résultats clés

- **4 profils de consommation** identifiés : critique (780 MW), forte, normale, basse  
- **Random Forest** : F1 = 0.788 (critique), variable la plus importante = `hour`  
- **SARIMA** : MAE = 180.8 MW, prévision à 7 jours avec IC 95 %  
- **Risques de surcharge** détectés principalement entre 18h et 22h en saison sèche  

---

## Site vitrine (Dashboard)

Un **site statique HTML/CSS/JS** est fourni dans le dossier `presentation/`. Il permet de visualiser les résultats sans PowerPoint et inclut une zone secrète de **questions de soutenance** (double‑clic sur l’onglet « Livrables »).

Ouvrez simplement `presentation/site.html` dans un navigateur.

---

## 👥 Équipe projet (Groupe #07)

| Rôle                 | Membre               |
|----------------------|----------------------|
| Chef de projet       | AAT Ndongo           |
| Rapport & EDA        | EVENGUE Philomène    |
| ACP & Clustering     | HALIMATOU SADIYA     |
| Classification       | IVANA                |
| SARIMA & Validation  | ETIA PATRICK         |

---

## Licence & remerciements

Projet réalisé dans le cadre du cours **Analyse de Données 2** de l’ENSPD.  
Merci à M. FOTSO Valdez pour l’encadrement.

*Toute reproduction doit conserver la mention de l’école et des auteurs.*
```
