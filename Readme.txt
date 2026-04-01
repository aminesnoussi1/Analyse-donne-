#  Analyse de Clustering & Réduction de Dimension — WeatherAUS

Ce projet applique des méthodes de **clustering non supervisé** et de **réduction de dimension (PCA)** sur le dataset météorologique **WeatherAUS**.  
L’objectif est d’explorer la structure interne des données, d’identifier des groupes naturels et d’améliorer la qualité du clustering grâce à la PCA.

---

##  1. Description du dataset

- **142 193 observations**
- **21 variables météorologiques** : températures, humidité, vent, pression, nuages, pluie…
- Variable cible disponible mais **non utilisée** : `RainTomorrow`

---

##  2. Prétraitement des données

###  Imputation
- Variables numériques → **médiane**
- Variables catégorielles → **modalité la plus fréquente**

###  Encodage
- Toutes les colonnes catégorielles ont été **factorisées** (codes entiers)

###  Normalisation
- StandardScaler appliqué sur **toutes les variables**
- Résultat : données centrées-réduites, prêtes pour la PCA

---

##  3. PCA — Analyse en Composantes Principales

### Variance expliquée
- PC1 ≈ **25 %**
- 10 premières composantes ≈ **85 %**
- 15 premières composantes ≈ **95 %**

### Choix final
 **Conservation de 15 composantes**, car elles capturent ~95 % de l’information totale.

### Résultat
- Dimensions initiales : **21**
- Dimensions après PCA : **15**

---

##  4. Interprétation des composantes

###  Inertie du premier axe
- PC1 explique **≈ 25 %** de la variance totale  
- C’est l’axe le plus informatif du dataset

###  Contribution du premier individu
- Contribution ≈ **faible (≈ 6 %)**  
- L’individu n’influence pas fortement PC1

###  Qualité de représentation
- Qualité ≈ **2 %**  
- L’individu est **mal représenté** par PC1 seul

---

##  5. Matrice de corrélation variables ↔ composantes

- Températures (`MinTemp`, `MaxTemp`, `Temp9am`, `Temp3pm`) fortement corrélées à **PC1**
- Pressions (`Pressure9am`, `Pressure3pm`) fortement corrélées à **PC2**
- Variables de vent corrélées à **PC3–PC5**
- Nuages et pluie corrélés à **PC5–PC7**

 La PCA révèle des **axes météorologiques cohérents** : température, pression, vent, humidité…

---

##  6. Clustering après PCA

Le meilleur algorithme identifié dans TD2‑3 était :

###  **Clustering hiérarchique (Ward)**

Il a été réappliqué sur les données réduites (15 composantes PCA).

### Résultats :
- Clusters plus compacts  
- Moins de bruit  
- Séparation plus nette  
- Structure plus lisible dans l’espace réduit

 **La PCA améliore la qualité du clustering.**

---

##  7. Conclusion

- La PCA permet de réduire la dimension de 21 → 15 tout en conservant 95 % de l’information  
- Les premières composantes capturent l’essentiel de la structure météorologique  
- Le clustering hiérarchique (Ward) reste la méthode la plus performante  
- La combinaison **PCA + Ward** donne les meilleurs résultats

---

