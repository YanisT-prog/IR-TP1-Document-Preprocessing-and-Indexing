# IR-TP1-Document-Preprocessing-and-Indexing

Recherche d'Information, séance de travail 1 (Master 2).

## Exécution
1. Ouvrir `tp1_preprocessing_indexing.ipynb` dans Google Colab ou Jupyter.
2. `pip install -r requirements.txt` (la liste des mots vides NLTK est téléchargée automatiquement).
3. Exécuter toutes les cellules. Les sorties sont écrites dans `results/`.

## Choix d'implémentation
- Tokenisation : `lower()`, `re.sub(r"[^\w\s]", " ", text)`, `split()`.
- Versions : A (minuscules + ponctuation), B (A + mots vides), C (B + racinisation de Porter).
- Vocabulaire, matrices binaire et TF, index inversé positionnel et `search_term()` sont implémentés à la main ; NLTK sert uniquement aux mots vides et au stemmer de Porter ; pandas uniquement à l'affichage et à l'export CSV.
- Les positions sont indexées à partir de 0 et se rapportent aux listes de tokens traitées.

## Résultats principaux
| Version | Vocabulaire | Tokens/doc (moy.) | Postings | Positions |
|---|---|---|---|---|
| A | 36 | 6,9 | 66 | 69 |
| B | 30 | 6,1 | 59 | 61 |
| C | 24 | 6,1 | 57 | 61 |

## Interprétation
Le prétraitement réduit le vocabulaire et l'index. La mise en minuscules et la suppression de la ponctuation (A) donnent 36 termes en fusionnant les variantes de casse comme « Information » et « information ». La suppression des mots vides (B) ramène le vocabulaire à 30 termes, la longueur moyenne de 6,9 à 6,1 tokens par document et les postings de 66 à 59, tout en décalant les positions. La racinisation (C) réduit encore le vocabulaire à 24 termes et les postings à 57, en regroupant retrieval, retrieve et retrieves sous « retriev », sans changer le nombre de positions stockées (61). Le rappel s'améliore, car une requête couvre plusieurs formes d'un mot. Ces gains ne sont pas systématiques : la racinisation peut fusionner des mots sans lien ou produire des racines illisibles comme « searchabl », et la suppression des mots vides empêche les requêtes par expression exacte. Le choix dépend donc de la tâche.
²²
