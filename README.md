# RAG médical sur MedQuAD

Projet d'IA hybride (ISIS Castres), sujet 2. Système de questions-réponses sur des textes médicaux du NIH : recherche (BM25, dense, hybride), génération avec citations par un modèle local (Ollama), refus et règles de sécurité.

Auteures : Yasmine Belarbi, Johanna Atymmo.

## Contenu du dossier

- `data/` : `medquad.csv` (jeu de données d'origine), `corpus.csv` (2 349 réponses retenues), `chunks.json` (4 829 chunks), `questions_test.json` (30 questions de test), `embeddings_minilm.npy` (vecteurs des chunks).
- `notebooks/` : `01_exploration.ipynb` (nettoyage, corpus, chunks, jeu de test) et `02_retrieval.ipynb` (recherche, seuil, règles de sécurité, génération, évaluation).
- `resultats/` : résultats du modèle avec les consignes v1 et v2, résultats sans recherche documentaire, notes de fidélité.
- `requirements.txt` : librairies Python et leurs versions.

## Installation

1. Créer et activer un environnement virtuel :
   ```
   python -m venv .venv
   .venv\Scripts\Activate.ps1
   ```
2. Installer les librairies :
   ```
   pip install -r requirements.txt
   ```
3. Installer Ollama (https://ollama.com) puis télécharger le modèle :
   ```
   ollama pull llama3.2:3b
   ```

## Utilisation

1. Ouvrir `notebooks/01_exploration.ipynb` et lancer toutes les cellules. Il crée `corpus.csv`, `chunks.json` et `questions_test.json` à partir de `medquad.csv`.
2. Ouvrir `notebooks/02_retrieval.ipynb`. La première cellule recharge les données et les embeddings, donc il faut la lancer en premier après chaque redémarrage du notebook. Le calcul des embeddings prend environ 5 minutes la première fois.
3. Pour la génération, l'application Ollama doit être lancée. Lancer les 30 questions avec le modèle prend environ 15 minutes.

Choisir le noyau Python du dossier `.venv` dans les notebooks.

## Paramètres retenus

- Recherche hybride : alpha = 0,8
- Seuil de refus sur le meilleur score dense : 0,57
- Modèle : `llama3.2:3b`, température 0, 3 passages donnés au modèle

## Remarques

- Le jeu de données MedQuAD est à télécharger sur Kaggle : https://www.kaggle.com/datasets/pythonafroz/medquad-medical-question-answer-for-ai-research
- Ce projet est un exercice. Il ne doit pas servir à donner des conseils médicaux.