Projet Fil Rouge – Analyse Comparative du Marché Airbnb
Madrid vs Barcelona
1. Objectif du projet

Ce projet vise à concevoir une solution data complète de bout en bout permettant de comparer le marché Airbnb entre Madrid et Barcelona, dans une logique d’aide à la décision pour un investisseur immobilier.

Le projet couvre l’ensemble du cycle de vie de la donnée :

Collecte → Nettoyage → Modélisation → Analyse → KPI → Base analytique → Visualisation

2. Problématique métier

L’objectif est de répondre aux questions suivantes :

Existe-t-il une différence significative entre les prix Airbnb à Madrid et Barcelona ?
Quelle ville présente un positionnement premium ?
Quelle ville offre davantage d’opportunités accessibles ?
Le type de logement influence-t-il significativement le prix ?
3. Indicateurs analysés (KPI)

Les principaux indicateurs étudiés sont :

Prix moyen par ville
Médiane des prix
Nombre total de logements
Prix moyen par type de logement
Disponibilité annuelle moyenne
Relation entre prix et disponibilité
Test statistique de comparaison des moyennes
4. Sources de données

Les données proviennent de la plateforme Inside Airbnb :

listings.csv
calendar.csv
reviews.csv
neighbourhoods.csv

Villes étudiées : Madrid, Barcelona
Date de collecte : 02/11/2026

5. Architecture du projet
data/
├── raw/            → données brutes
├── processed/      → données nettoyées, exports KPI, base SQLite

notebooks/
├── 01_listings_merge_v2.ipynb
├── 02_extraction_eda_v2.ipynb
├── 03_database_modeling.ipynb
├── 04_data_model_star_schema.ipynb
├── 05_sql_kpis_star_schema.ipynb

docs/
├── cadrage_metier.md
├── cahier_des_charges_data.md
├── sources.md
6. Pipeline de traitement des données
6.1 Fusion des données

Fusion des datasets Madrid et Barcelona avec création d’une variable city.

6.2 Nettoyage et préparation
Suppression des valeurs manquantes critiques
Traitement des valeurs aberrantes via le 99e percentile
Harmonisation des variables
Export vers listings_clean.csv
6.3 Analyse exploratoire (EDA)
Analyse descriptive
Distribution des prix
Segmentation par type de logement
Comparaison entre villes
6.4 Validation statistique

Test t de Student (Welch) :

p-value < 0.05
Différence statistiquement significative
Barcelona présente des prix moyens supérieurs à Madrid
6.5 Modélisation analytique

Mise en place d’une base SQLite en schéma en étoile :

fact_listings
dim_city
dim_room_type

Objectif : structurer les données pour une exploitation BI.

6.6 Calcul des KPI en SQL

Calcul des indicateurs directement dans la base analytique, avec export vers :

data/processed/

7. Résultats principaux
Barcelona présente un positionnement plus premium
Madrid offre des opportunités plus accessibles
Les logements de type "Entire home/apt" tirent les prix vers le haut
La corrélation entre prix et disponibilité est faible
La différence de prix entre les deux villes est statistiquement significative
8. Conclusion métier

Pour un investisseur :

Barcelona correspond à une stratégie haut de gamme
Madrid permet un positionnement plus accessible
La segmentation par type de logement est un facteur clé dans la stratégie d’investissement
9. Stack technique
Python
Pandas / NumPy
Matplotlib / Seaborn
SciPy (tests statistiques)
SQLite (base analytique)
SQL (KPI)
Jupyter Notebook
Git / GitHub
