# YouTube Trending Prediction – README 

Ce projet explore plusieurs modèles de Machine Learning afin de **prédire si une vidéo YouTube va devenir tendance** à partir de métadonnées disponibles dès la publication.

## Utilisation rapide

# Installation
pip install -r requirements.txt

# Entraînement
python train.py --model xgboost

# Prédiction
python predict.py --video "path/to/video.json"

---

## 1. Meilleur modèle

| Item          | Valeur |
|---------------|--------|
| **Modèle**    | **XGBoost** |
| **Accuracy**  | 0.9929 |
| **Precision** | 1.0000 |
| **Recall**    | 0.9647 |
| **F1-Score**  | 0.9820 |

**Pourquoi ?**  
XGBoost atteint les **meilleurs scores sur toutes les métriques** et fournit une **interprétabilité claire** via l’importance des variables. Son algorithme de boosting capture finement les interactions non-linéaires entre les features.

---

## 2. Variables les plus importantes

1. **Nombre de vues** (73 %)  
   *Plus il y a de vues, plus la vidéo a de chances d’être tendance.*
2. **Catégorie de la vidéo** (10 %)  
   *Gaming ou musique ? Ces catégories ont souvent la cote.*
3. **Engagement global** (6 %)  
   *Likes + commentaires divisés par les vues : une vidéo « vivante ».*

Toutes les autres (longueur du titre, heure de publication, etc.) ont un petit rôle.

---

## 3. Limitations (en clair)

- Le modèle regarde **surtout le nombre de vues**.  
- On ne lit pas encore **le texte du titre ou de la description**.  
- On ne sait pas si une vidéo est en train de **monter ou de redescendre**.  
- Peu de vidéos « tendance » dans le jeu de données → le modèle n’a pas beaucoup d’exemples.

---

## 4. Améliorations suggérées

| **Mieux utiliser les vues** | Eviter que le modèle dise « beaucoup de vues = tendance » sans regarder le reste. | Diviser les vues par le temps depuis la publication ou utiliser une échelle logarithmique. |
| **Ajouter l’intelligence du titre** | Les mots-clés comme « TikTok », « réaction » ou « tutoriel » aident à prédire. | Compter les mots tendance dans le titre avec un simple script Python. |
| **Regarder la vitesse des vues** | 1 000 vues en 1 h signifie plus que 1 000 vues en 1 mois. | Calculer « vues par heure » depuis la mise en ligne. |
| **Tester d’autres heures** | Publier à 3 h du matin VS 19 h, ce n’est pas pareil. | Ajouter des colonnes « jour de la semaine » et « heure ». |
| **Mélanger deux modèles** | Utiliser la force d’XGBoost + la finesse d’un réseau de neurones. | Faire un vote entre plusieurs modèles (stacking simple). |

---

## 5. Apprentissages clés

- **Transformer** les données (log, ratio, heure) aide beaucoup.  
- **Tester plein d’idées simples** donne souvent de meilleurs résultats qu’un seul modèle compliqué.
