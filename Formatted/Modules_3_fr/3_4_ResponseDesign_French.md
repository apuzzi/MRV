---
title: Plan de réponse
summary: Ce tutoriel présente le concept de plan de réponse, énumère les termes importants et met en évidence différents outils qui peuvent être utilisés pour la collecte d'observations de référence dans le contexte de l'estimation de superficie et de la précision des cartes. D'autres tutoriels peuvent être trouvés ici sur OpenMRV sous le processus " Collecte de données d'échantillon " et les outils " GEE ", " AREA2 ", " CE ", et " CEO 
author: Pontus Olofsson
creation date: Février, 2021
language: Français
publisher and license: Copyright 2021, Banque mondiale. Cette œuvre est protégée par une licence Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- GEE
- AREA2
- CEO
- CE
- Stratifié
- Simple aléatoire
- Systématique
- Plan de réponse
- Sondage
- Plan de sondage
- Données de référence
- Classification de référence
- Observations de référence
- Mozambique
- Cambodge

group:
- catégorie : Collect Earth
  étape : Collecte de données de référence
- catégorie : Collect Earth Online
  étape : Collecte de données de référence
- catégorie : GEE
  étape : Collecte de données de référence
---


# Plan des réponses

## 1 Contexte

Le plan de réponse définit la " réponse " des unités d'un échantillon. Dans le cadre de l'inférence basée sur le plan de sondage dans un contexte géographique, " le plan de sondage englobe toutes les étapes du protocole qui conduisent à une décision concernant la concordance entre les classifications de référence et cartographiques et la meilleure classification disponible des conditions d'occupation des sols pour chaque unité spatiale échantillonnée " (Olofsson et al. 2014). Les termes suivants sont importants :

**Données de référence** 

Données caractérisant l'évaluation la plus précise possible de la condition réelle à l'emplacement de l'échantillon (exemple : imagerie satellite à haute résolution).

**Les observations de référence** 

L'évaluation la plus exacte possible de l'état réel d'une unité de population.

**Reference classification** 

La classification de référence appliquée à la collection de toutes les unités d'échantillonnage.

Ici, sur OpenMRV, sous " Collecte de données d'échantillons " et les outils " GEE ", " AREA2 ", " CE " et " CEO ", vous trouverez des tutoriels où vous apprendrez à déterminer les conditions de référence. Nous allons examiner les unités d'un ensemble de données d'échantillon. Cet ensemble de données d'échantillon aura quatre strates : forêt, non-forêt, perturbation de la forêt et une zone tampon autour de la perturbation de la forêt. 
L'objectif est d'estimer la zone de perturbation forestière ; par conséquent, vous allez apprendre à collecter des observations de référence de *forêt, non-forêt* et *perturbation forestière*. Ceci est démontré à l'aide de trois outils différents parmi lesquels l'utilisateur peut choisir : GEE/AREA2, Collect Earth Desktop et Collect Earth Online.

### 1.1 Tutoriels

- Pour le plan de réponse utilisant **AREA2**, veuillez vous référer au processus "Collecte des données de l'échantillon" et aux outils "AREA2" et "GEE" ici sur OpenMRV.
- Pour le plan de réponse utilisant **Collect Earth Desktop**, veuillez vous référer au processus " Collecte des données de l'échantillon " et à l'outil " CE " ici sur OpenMRV.
- Pour le plan de réponse utilisant **Collect Earth Online**, veuillez vous référer au processus " Collecte des données de l'échantillon " et à l'outil " CEO " ici sur OpenMRV.

### 1.2 Terminologie additionnelle

**Plan de réponse**

Défini par (Stehman and Czaplewski, 1998): “La référence ou classe réelle est obtenue pour chaque unité d'échantillonnage sur la base de l'interprétation de photographies aériennes ou de vidéographies, d'une observation au sol ou d'une combinaison de ces sources. Les méthodes utilisées pour déterminer cette référence de classification sont appelées "plan de réponse". Le plan d'intervention comprend les procédures de collecte des informations relatives à la détermination de la occupation du sol de référence, et les règles d'attribution d'une ou plusieurs [labels] de référence à chaque unité d'échantillonnage.” Connu sous le nom de “plan de mesure” par Särndal et al. (1992).

**Echantillon**

Un sous-ensemble de la population sélectionné parmi les unités de la population.

**Plan d'échantillonnage**

Synonyme de plan d'échantillonnage (Sampling Design), qui est le terme préféré dans la littérature de référence (Cochran, 1977, Särndal et al., 1992). Le terme apparaît chez Rice (1995) ui utilise à la fois “plan d'echantillonnage” et “plan d'echantillon”.

**Plan d'échantillonnage**

“Le concept de plan d'échantillonnage (sampling design ) est le protocole par lequel les unités de référence de l'échantillon sont sélectionnées” (Stehman and Czaplewski, 1998). Le terme “Sampling design” est également utilisé par Cochran (1977) and Särndal et al. (1992) -- Le premier utilise également “sampling plan”.

**Sondage/Enquête**

Särndal et al. (1992) définissent une enquête comme une “investigation partielle d'une population finie”, et précisent que “les concepts d ‘enquête’ et ‘enquête par sondage’ sont utilisés pour désigner des enquêtes statistiques présentant les caractéristiques méthodologiques suivantes: [...] échantillonnage aléatoire [...] plan de mesure [et] estimation”. de facon plus precise une enquete par sondage ou un sondage est une enquête effectuee sur une partie de la population. Cette fraction de la population constitue l'échantillon et les méthodes qui permettent de construire cet echantillon s'appellent méthode d'échantillonnage.

**Plan d'enquête**

Un “plan de sondage total” définit les procédures pour “obtenir la plus grande précision possible dans les estimations de l'enquête tout en trouvant un équilibre entre les erreurs d'échantillonnage et les erreurs non dues à l'échantillonnage [...] Le plan de sondage donne lieu à des opérations d'enquête” sélection de l'échantillon (Särndal et al., 1992). Lohr (1999) décrit un plan de sondage total comme “Une philosophie de conception d'enquête visant à minimiser les erreurs de non-échantillonnage ainsi que les erreurs d'échantillonnage..” De plus, dans Lohr (1999) “plan d'enquête” est synonyme de plan d'échantillonnage.

## 2 Références

Cochran, W.G., 1977. *Sampling Techniques*, John Wiley & Sons, New York, NY.

Lohr, S.L., 1999. *Sampling: Design And Analysis,* CRC Press.

Olofsson, P., Foody, G.M., Herold, M., Stehman, S.V., Woodcock, C.E. and Wulder, M.A., 2014. Good practices for estimating area and assessing accuracy of land change. Remote Sensing of Environment, 148, pp.42-57. https://doi.org/10.1016/j.rse.2014.02.015

Rice, J.A., 1995. *Mathematical Statistics and Data Analysis* (2nd ed.), Duxbury Press, Belmont, CA.

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. *Model assisted survey sampling*, Springer Science & Business Media, New York, NY.

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8

------

[![img](./figures/cc.png)](./figures/cc.png)

Cette œuvre est soumise à une licence [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/).

Copyright 2021, Banque Mondiale

Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la notification et la vérification pour soutenir la mise en œuvre du MRV dans les pays.

Attribution  
Olofsson, P. 2021. Response Design. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/wb_fcfc_gfoi.png)
