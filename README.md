# Scoring Prospects Smart4 Engineering

Ce projet porte sur un outil de scoring commercial basé sur l'historique des missions Smart4 Engineering (plateforme Whoz). 
Le modèle estime la probabilité de succès d'un prospect à partir de ses caractéristiques (entité, délais, priorité, contexte de l'entité).

J'ai réalisé ce projet dans le cadre de mon mémoire de fin d'études M2 Data & IA à Nexa Digital School, en alternance en tant que BI Analyst chez Smart4 Engineering.

**Application déployée** : https://smart4-scoring-staffing.streamlit.app/

## Confidentialité

Les données utilisées pour ce projet appartiennent à Smart4 Engineering et sont extraites de sa base Whoz (Azure SQL Data Lake). Dans le cadre de ce mémoire, l'entreprise n'autorise pas la diffusion de cette base, des données brutes ou traitées, ni du code d'extraction (requêtes SQL et accès au Data Lake).

Ce dépôt contient donc uniquement :
- le code de modélisation (entraînement, comparaison des modèles, évaluation)
- le code de l'application Streamlit

La partie extraction (connexion Azure SQL, requêtes de jointure et d'agrégation) n'est pas incluse. 
Les dossiers de données ne sont pas fournis non plus. 
Pour rappel, dès l'extraction, les identifiants sensibles (mission, workspace) sont systématiquement hashés en SHA-256, et aucune donnée nominative (nom de consultant, nom de client) n'entre dans le pipeline.

## Structure du dépôt

-> app.py application Streamlit
-> scoring.py fonctions de scoring et de calcul SHAP
-> model_scoring_prospects.joblib modèle entraîné
-> mappings.json mappings des variables catégorielles (entités, priorité...)
-> win_ratio_par_entite.csv taux de succès historique par entité
-> style.css style et esthétique de l'application
-> requirements.txt
-> README.md

## Pipeline

Le code d'extraction (SQL, connexion Azure) n'étant pas inclus dans ce dépôt, le pipeline présenté ici démarre à partir du jeu de données déjà extrait :
1. Nettoyage : exclusion des missions issues d'imports en masse (biais de survie)
2. Feature engineering : écarts de dates, priorité encodée, agrégats de certifications par entité
3. Entraînement et comparaison de plusieurs modèles (régression logistique, arbre de décision, random forest, XGBoost, SVM)
Modèle retenu : Random Forest (AUC-ROC 0.9614, F1=0.84).

## Application

Application Streamlit permettant de saisir les caractéristiques d'un prospect et d'obtenir une probabilité de succès, une zone de score, et une explication SHAP.

## Installation
## Scoring des besoins de staffing Smart4 Engineering

Ce projet porte sur un outil de scoring commercial basé sur l'historique des missions Smart4 Engineering (plateforme Whoz). 
Le modèle estime la probabilité de succès d'un besoin de staffing à partir de ses caractéristiques (entité, délais, priorité, contexte de l'entité).

J'ai réalisé ce projet dans le cadre de mon mémoire de fin d'études M2 Data & IA à Nexa Digital School, en alternance en tant que BI Analyst chez Smart4 Engineering.

**Application déployée** : https://smart4-scoring-staffing.streamlit.app/

## Disclaimer : Protection des données personnelles (RGPD)

**Avertissement important sur les données utilisées dans cette thèse**

Ce projet est né d'un vrai besoin identifié au sein du Groupe Smart4 Engineering. Les données exploitées proviennent du Data Lake interne de l'entreprise. Conformément au Règlement Général sur la Protection des Données (RGPD, Règlement (UE) 2016/679), toutes les données à caractère personnel ont été anonymisées avant tout traitement analytique.

Les mesures appliquées sont les suivantes :
- Suppression de toutes les colonnes directement identifiantes (noms, emails, téléphones...)
- Pseudonymisation des identifiants techniques par hachage SHA-256 directement sous SQL, avant même de quitter le Data Lake : aucun identifiant brut ne transite par un fichier intermédiaire
- Généralisation des valeurs précises en intervalles ou catégories
- Agrégation des métriques individuelles sensibles au niveau groupe

Ce document académique ne contient aucune donnée nominative, aucune information contractuelle confidentielle, et aucun résultat permettant d'identifier un individu. Les noms réels des entités du groupe ont également été remplacés par des codes génériques partout dans ce document, y compris dans les tableaux de résultats.

Conformément aux accords conclus avec le Groupe Smart4 Engineering et validés avec l'encadrement pédagogique, aucun fichier de données réelles (extraction brute ou dataset transformé) n'est distribué avec ce mémoire, de même que le code d'extraction (requêtes SQL, connexion au Data Lake), pour des raisons de confidentialité.

Sont fournis : le code de modélisation, le code de l'application, le modèle déjà entraîné et un dictionnaire de correspondances.

## Accès et identifiants

L'application est accessible publiquement, sans authentification ni identifiants de test : https://smart4-scoring-staffing.streamlit.app/

Elle ne dispose pas de back-office administrateur : c'est une interface de scoring en lecture, sans espace de gestion séparé.

La connexion à la base SQL (Azure SQL Data Lake) n'est utilisée que côté extraction, en amont du pipeline, dans un environnement interne à Smart4 Engineering. Elle ne fait pas partie du périmètre de l'application déployée, pour les raisons de confidentialité détaillées ci-dessus.

**Compatibilité navigateurs** : testée sur Google Chrome (dernière version).

## Structure du dépôt

-> app.py application Streamlit

-> scoring.py fonctions de scoring et de calcul SHAP

-> model_scoring_staffing.joblib modèle entraîné

-> mappings.json mappings des variables catégorielles (entités, priorité...)

-> win_ratio_par_entite.csv taux de succès historique par entité

-> style.css style et esthétique de l'application

-> requirements.txt

-> README.md

## Pipeline

Le code d'extraction (SQL, connexion Azure) n'étant pas inclus dans ce dépôt, le pipeline présenté ici démarre à partir du jeu de données déjà extrait :
1. Nettoyage : exclusion des missions issues d'imports en masse (biais de survie)
2. Feature engineering : écarts de dates, priorité encodée, agrégats de certifications par entité
3. Entraînement et comparaison de plusieurs modèles (régression logistique, arbre de décision, random forest, XGBoost, SVM)

Modèle retenu : Random Forest (AUC-ROC 0.9614, F1=0.836).

## Application

Application Streamlit permettant de saisir les caractéristiques d'un besoin de staffing et d'obtenir une probabilité de succès, une zone de score, et une explication SHAP.

## Prérequis et installation

conda create -n scoring-app python=3.10
conda activate scoring-app
pip install -r requirements.txt
streamlit run app.py
conda create -n scoring-app python=3.10
conda activate scoring-app
pip install -r requirements.txt
streamlit run app.py
