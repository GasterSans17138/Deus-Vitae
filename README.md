# Deus Vitae - README

**Auteurs** : Ce projet a été fait par 3 programmeurs : Eliot Nerrand, François Lahalle et Christophe Huang, ainsi que 3 artistes : Kenza Druart, Nicolas Roland et Chanelle Mazenq.

**Deus Vitae** est un prototype Unreal Engine 5 qui met en œuvre plusieurs systèmes clés pour animer dynamiquement un environnement désertique :

- **Procédural Content Generation (PCG)** en temps réel
- **Génération et animation de la flore** (croissance, montée des eaux)
- **Système IA** pour prédateur (léopard) et troupeau (zèbres)
- **Flocking** (illusion de groupe)
- **Post-traitement visuel** (brouillard, halo, FOV dynamique)

---

## Table des matières
1. [Utilisation](#utilisation)
2. [Fonctionnalités](#fonctionnalit%C3%A9s)
   - [Procédural Content Generation](#proc%C3%A9dural-content-generation)
   - [Flore dynamique](#flore-dynamique)
   - [Système IA (State Tree)](#syst%C3%A8me-ia-state-tree)
   - [Flocking](#flocking)
   - [Effets visuels et PostProcess](#effets-visuels-et-postprocess)
3. [Améliorations possibles](#am%C3%A9liorations-possibles)

---

## Utilisation
1. Ouvrir la map **L_François** dans l’éditeur Unreal Engine 5.5.
2. Lancer la scène via le bouton **Play**.
3. Se déplacer pour observer :
   - la génération de la flore procédurale autour du joueur.
   - le comportement IA des animaux (léopard et troupeau de zèbres).
4. Ajuster les paramètres dans les panneaux **PCG** et **PostProcess** selon les besoins.

---

## Fonctionnalités

### Procédural Content Generation
- Utilisation du plugin PCG Component pour générer des points et spawner des `StaticMesh` autour du joueur.
- Spline dynamique en mode Play, mise à jour sans régénération totale.
- Filtrage par type de terrain (pente, eau, sol) et densité contrôlée.
- Optimisations : réduction de polys, suppression progressive des anciens meshes.

### Flore dynamique
- Croissance animée des plantes et arbres via `Spline Actor` C++.
- Intégration du plugin **Water** pour lacs et rivières, avec animation du niveau d’eau.
- Affichage de la zone d’influence du PCG autour du joueur.

### Système IA (State Tree)
- Deux comportements :
  - **Léopard (prédateur)** : détection, poursuite et attaque d’une cible.
  - **Zèbre (proie)** : fuite et illusion de troupeau.
- Implémentation en Blueprints State Tree avec tâches, transitions et variables.
- Scoring aléatoire pour prioriser les états (errer, dormir, attaquer, s’enfuir).

### Flocking
- Système de leader pour guider le groupe de zèbres.
- Mouvement coordonné sans calcul d’essaims multiples.

### Effets visuels et PostProcess
- **PostProcess Volume** pour ajouter un brouillard basé sur la profondeur.
- **Post Material** custom pour contrôler densité et couleurs.
- Contrôle dynamique du **FOV** en C++.
- **Halo lumineux** sur le personnage via UV animées.

---

## Captures d’écran
Voici quelques captures du prototype en action :

- [Screenshot 1 – Léopard et zèbres](Screenshots/Arcturus%20-%20Unreal%20Editor%2015_07_2025%2017_44_27.png)
- [Screenshot 2 – Vue d’ensemble](Screenshots/Arcturus%20-%20Unreal%20Editor%2015_07_2025%2017_44_52.png)
- [Screenshot 3 – Troupeau au loin](Screenshots/Arcturus%20-%20Unreal%20Editor%2015_07_2025%2017_47_04.png)

---


## Améliorations possibles
- Partitionnement du landscape pour de meilleures performances.
- PCG Instances séparées par type de mesh.
- Multi-troupeaux et MoveTo modulaire.
- Depth of Field et transitions FOV plus fluides.
- Variations de densité et de couleur du brouillard.
