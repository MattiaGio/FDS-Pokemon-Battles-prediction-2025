[![Kaggle](https://img.shields.io/badge/Kaggle-20BEFF?logo=kaggle&logoColor=fff)](#)
[![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=fff)](#)
![Linear Regression](https://img.shields.io/badge/Linear%20Regression-Gen1%20Predictor-FFD700?style=for-the-badge&logo=pokemon&logoColor=black)
![CatBoost](https://img.shields.io/badge/CatBoost-Gen1%20Predictor-FF0000?style=for-the-badge&logo=pokemon&logoColor=yellow)
![Gen 1 Pokémon](https://img.shields.io/badge/Pokémon-Gen%201-9CA3AF?style=for-the-badge&logo=nintendo-game-boy&logoColor=white)


# 🎮 FDS-Pokemon-Battles-prediction-2025

Challenge for Foundation of Data Science.\
The goal is to predict the winner of a Pokémon battle in Gen1 OU, given the first 30 turns of a real game.

**Kaggle Challenge URL:**\
www.kaggle.com/competitions/fds-pokemon-battles-prediction-2025/overview/citation

------------------------------------------------------------------------

## 🚀 Our Approach

Our first idea was to teach a model how to play Pokémon battles by engineering a large number of features, aiming to capture as many
mechanics, strategies, and edge cases as possible.

However, during experimentation, we noticed that the local validation score was increasing very slowly and did not match our expectations.
After encountering clear signs of overfitting, we realised the model was being fed many redundant or unnecessary features. This led to the model
plateauing at around \~83% accuracy.

------------------------------------------------------------------------

## ✨ The Realisation --- *"Less is More"*

We then shifted our focus toward feature selection---keeping only the features that truly mattered instead of overloading the model.

After analysing the top 30 most important features, we discovered two natural feature clusters:

-   🔮 **"Future" features**\
-   📊 **"Updated" features**

We trained a model using the "future" features and noticed that including information about the 30th turn, like the latest status, Pokémon left, moves used, and more, significantly improved both accuracy and stability.

The "updated" cluster combined "future" features with meaningful game statistics such as average HP per player, start percentage, faint difference, and more. Training a model on this feature set yielded our best performance so far, with consistent improvements.

------------------------------------------------------------------------

## 🏆 The Final Choice

In the last days, we focused on refining the "future" model by adding additional features such as each player's remaining Pokémon and available moves. We then trained this version using Logistic Regression and CatBoost, and submitted both the "future" and "updated" models.

------------------------------------------------------------------------

## 👥 Participants

-   [Valerio Mesiti\ @ValerioM01](https://github.com/ValerioM01)
-   [Gabriele Moretti\ @gabmor01](https://github.com/gabmor01)
-   [Mattia Giordano](https://github.com/MattiaGio)

------------------------------------------------------------------------

# 🔍 Code Deep Dive

We produced **3 different notebooks**:

-   **BEST_solo_futuro_0.8473**\
-   **notebook_logreg**\
-   **solo_futuro_pp_catboost**

------------------------------------------------------------------------

## 📘 Common Structure

We have created a dictionary with SOME Pokémon information. We have decided to keep the most relevant, plus some that will update the last
status of that Pokémon.

We also added a TypeChart dictionary to retrieve *"STAB"* and *"super effective"* moves, and a list of the best moves the Pokémon in the
dictionary could use.

We have trained:

-   **BEST_solo_futuro_0.8473** → Logistic Regression (5-Fold)\
-   **notebook_logreg** → Logistic Regression (5-Fold)\
-   **solo_futuro_pp_catboost** → CatBoost (5-Fold)

------------------------------------------------------------------------

## 🔮 BEST_solo_futuro_0.8473

This notebook extracts features that represent what has been left at the end of the 30th turn---key to this notebook and to *solo_futuro_pp_catboost*.

Extracted features include:

-   Extraction of the Pokémon and the state of both teams\
-   Counter for the faints of both teams\
-   Moves used for both teams\
-   HP remaining for both teams\
-   Min/max/avg values for the stats of both teams

------------------------------------------------------------------------

## 📊 notebook_logreg

This model has some different features, more basic, with a couple of complex stats, like:

-   a damage calculator of each move\
-   a real speed extractor of the Pokémon on the field (to determine who
    starts first)\
-   a volatile effect counter

It is trained using Logistic Regression.

------------------------------------------------------------------------

## 🔮 solo_futuro_pp_catboost

This model contains the same features as **BEST_solo_futuro_0.8473**, with the addition of a counter that tells the model how many best moves a Pokémon has left.

**Kaggle Notebook URL:**\
https://www.kaggle.com/code/mattiagiordano/notebook-to-submit-github-repo
