# Mandelatechno

Activités interactives de **Technologie au collège**, publiées en pages web pour être
utilisées sur ordinateur, tablette et téléphone.

**Adresse du site :** <https://pierredupuy80-chef.github.io/Mandelatechno/>

---

## Ce que contient le dépôt

```
index.html                                    page d'accueil : la liste des activités
.nojekyll                                     demande à GitHub de servir les fichiers tels quels
3e/ost1a/
    app-activite1-frise-evolution.html        1 · Frise interactive — 150 ans de communication
    app-activite2-innovations.html            2 · Innovations et ruptures technologiques
    app-activite3-biais-ia.html               3 · Simulateur LexIA — les biais de l'IA
```

Chaque application est un **fichier HTML autonome** : le style, le code et les images sont
inclus dans le fichier. Aucune bibliothèque externe n'est téléchargée, donc aucune activité
ne dépend d'un service tiers pour s'afficher.

---

## Activer GitHub Pages (une seule fois)

1. Ouvrir <https://github.com/pierredupuy80-chef/Mandelatechno/settings/pages>
2. Dans **Source**, choisir **Deploy from a branch**
3. Branche : **main**, dossier : **/ (root)**, puis **Save**
4. Attendre une à deux minutes : le site est en ligne à l'adresse ci-dessus

À chaque `git push` sur `main`, GitHub republie automatiquement le site en une minute environ.

---

## Ajouter une activité

1. Créer le dossier de la séquence, par exemple `4e/ost2/`
2. Y déposer le fichier `.html` de l'activité
3. Ajouter une carte dans `index.html`, sur le modèle des cartes existantes :

```html
<article class="carte">
  <h3>1 · Titre de l'activité</h3>
  <p>Une phrase qui décrit ce que l'élève va faire.</p>
  <span class="niveaux">N1 → N4</span>
  <a class="ouvrir" href="4e/ost2/mon-activite.html">Ouvrir l'activité</a>
</article>
```

4. Publier :

```bash
git add -A
git commit -m "Ajout de l'activité ..."
git push
```

---

## Compatibilité téléphone

Les trois applications ont été auditées puis corrigées pour l'usage au doigt
(détail complet dans le rapport d'audit du dossier de préparation) :

| Point | Avant | Après |
|---|---|---|
| Barre du haut, part de l'écran occupée en permanence | 39 à 66 % | 5 à 12 % |
| Barre du haut sur écran de 320 px | 400 px (66 %) | 67 px (12 %) |
| Éléments cliquables dont le tap partait dans la barre | jusqu'à 40 | 0 |
| Changement de niveau | restait au milieu de la page | revient en haut |
| Zoom automatique iOS à chaque saisie | tous les champs | supprimé (champs à 16 px) |
| Réponses de QCM trop petites à viser | jusqu'à 100 % | 0 |
| Exercices de glisser-déposer au doigt | impossibles (2 exercices) | toucher pour choisir, toucher pour placer |

Ce qui a été mis en place :

- la barre du haut **se replie au défilement** : le titre et les champs binôme/classe
  disparaissent vers le haut, seuls les onglets de niveau restent visibles (~46 px) ;
- les onglets tiennent **sur une seule ligne** et défilent horizontalement au doigt ;
- `scroll-padding-top` est calculé dynamiquement, donc les titres ne se cachent plus
  sous la barre ;
- le changement de niveau **remonte la page en haut** ;
- les exercices de glisser-déposer acceptent désormais le **toucher** (choisir puis placer),
  tout en conservant le glisser à la souris sur ordinateur ;
- les champs de saisie passent à **16 px** sur petit écran (seuil qui empêche iOS de zoomer) ;
- les réponses de QCM font au moins **44 px de haut**, la ligne entière étant cliquable.

Sur ordinateur, le rendu et le comportement sont **inchangés** : la barre reste collante et
les onglets reviennent à la ligne.

### Export PDF

Le bouton d'export utilise l'impression du navigateur. Il fonctionne sur **Chrome (Android,
Windows, macOS)**, **Safari (iPhone, iPad)** et **Edge**, mais **pas sur Firefox Android**.
À rappeler aux élèves qui travaillent sur téléphone.

---

## Vérifier avant de publier

Les scripts d'audit se trouvent dans le dossier de préparation du cours, sous `_outils/` :

```bash
node _outils/verifier_correctifs.js        # compare chaque app corrigée à sa sauvegarde
node _outils/preuve_interactions.js "chemin/vers/app.html" ".assoc-item" ".assoc-target"
node _outils/captures_mobile.js "chemin/vers/app.html"
```

Les sauvegardes `*.BACKUP-avant-correctifs-mobile.html` permettent de revenir en arrière et
servent de référence pour mesurer les gains.

---

## Données et vie privée

- Les activités **n'enregistrent rien sur un serveur** : les réponses sont stockées
  uniquement dans le navigateur de l'élève (`localStorage`).
- Aucun cookie, aucun traceur, aucune mesure d'audience n'est utilisé.
- Les liens vers les fiches, vidéos et quiz externes (Podeduc, Nuage, Google Forms) ne sont
  sollicités que si l'élève clique dessus ; ils nécessitent une connexion.

---

## Licence

MIT — voir [LICENSE](LICENSE).
