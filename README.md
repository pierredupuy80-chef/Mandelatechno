# Mandelatechno

Activités interactives de **Technologie au collège**, publiées en pages web pour être
utilisées sur ordinateur, tablette et téléphone.

**Adresse du site :** <https://pierredupuy80-chef.github.io/Mandelatechno/>

---

## Ce que contient le dépôt

```
index.html                          page d'accueil : les 21 pages, sommaire par niveau
.nojekyll                           demande à GitHub de servir les fichiers tels quels

3e/revision-ost1/                   Réviser l'évaluation — séquences 1a et 2a
    revision-evaluation.html        fiches de synthèse, lexique, méthode et 42 questions
3e/ost1a/                           OST 1 — le smartphone
    app-activite1-frise-evolution.html
    app-activite2-innovations.html
    app-activite3-biais-ia.html
3e/ost2a/app-impact-numerique.html  OST 2a — l'impact du numérique
3e/ost3/app-comparateur-ost.html    OST 3 — trottinette électrique et VAE
3e/rnr/app-tracker-solaire.html     RNR — tracker solaire
3e/tp-ia/                           TP d'apprentissage IA
    tp-ia.html
    atelier-ia-exemples.html        atelier « L'IA apprend avec des exemples »
    CREDITS-SONS.md                 crédits et licences des sons de l'atelier
    donnees/*.csv                   6 fichiers à ouvrir dans un tableur
3e/bonus-incident-ia/               Activité bonus — l'incident OpenAI / Hugging Face
    infographie-incident-ia.html    infographie à projeter et à commenter
    infographie-incident-ia.jpg     l'infographie (1536 × 1024, JPEG, 374 Ko)

4e/ost0/activite-iag-assistant.html               Séquence 0 — utiliser l'IAG
4e/ost1/activite-securite-donnees.html            Séquence 1 — sécurité des données
4e/ost2/activite-evolution-drones.html            Séquence 2 — les drones
4e/ost3/activite-maison-connectee-eclairage.html  Séquence 3 — maison connectée
4e/ost4/activite-chauffage-domotique.html         Séquence 4 — chauffage domotique

5e/ost2/activite-outils-numeriques.html           Séquence 2 — outils numériques
5e/ost3/activite-evolution-ost.html               Séquence 3 — évolution des OST
5e/ost4/activite-souris-interaction.html          Séquence 4 — la souris
5e/ost5/activite-choix-lampes.html                Séquence 5 — choisir un OST : les lampes
```

Une convention de nommage simple : `Niveau/ostN/` pour un objet et système technique,
`Niveau/tp-*/` pour un travail pratique. Le numéro suit celui de la séquence d'origine, ce qui
permet de retrouver le dossier de préparation correspondant.

Chaque application est un **fichier HTML autonome** : le style, le code, les images et même les
données et les sons sont inclus dans le fichier. Aucune bibliothèque externe n'est téléchargée,
donc aucune activité ne dépend d'un service tiers pour s'afficher. Seuls les liens vers les
fiches, vidéos et quiz externes nécessitent une connexion, et uniquement si l'élève clique.

---

## GitHub Pages

Le site est **en ligne** : <https://pierredupuy80-chef.github.io/Mandelatechno/>

À chaque `git push` sur la branche `main`, GitHub republie le site automatiquement en une
minute environ. La page d'accueil est `index.html` à la racine du dépôt.

Si le réglage devait être refait (par exemple pour un nouveau dépôt) :

1. Ouvrir <https://github.com/pierredupuy80-chef/Mandelatechno/settings/pages>
2. Dans **Source**, choisir **Deploy from a branch**
3. Branche : **main**, dossier : **/ (root)**, puis **Save**
4. Attendre une à deux minutes

---

## Ajouter une activité

1. Créer le dossier de la séquence, par exemple `4e/ost2/`
2. Y déposer le fichier `.html` de l'activité — **après** lui avoir appliqué le correctif
   mobile avec `_outils/appliquer_correctifs_mobile.py` (voir ci-dessous)
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

Les **17 mini-apps** (15 activités + les 2 pages du TP) ont été auditées dans un navigateur en
émulation de téléphone, puis corrigées pour l'usage au doigt. La page de l'activité bonus
(l'infographie de l'incident OpenAI / Hugging Face) est **hors de ce périmètre** : elle n'a
pas d'interaction au doigt, seulement une image et deux liens, et sa page se contente
d'afficher l'image sur toute la largeur — il n'y a donc rien à corriger pour le mobile. Chaque correction a été vérifiée
en comparant la page corrigée à sa sauvegarde `*.BACKUP-avant-correctifs-mobile.html`.

| Point | Avant | Après |
|---|---|---|
| Barre du haut, hauteur occupée en permanence (390×844) | 175 à 400 px | **31 à 65 px** |
| Barre du haut sur écran de 320 px | jusqu'à 400 px (66 %) | **31 à 65 px (8 à 12 %)** |
| Barre du haut en paysage | jusqu'à 169 px | **31 à 65 px** |
| Éléments cliquables dont le tap partait dans la barre | jusqu'à 40 | 0 à 7 (éléments sous la barre) |
| Changement de niveau | restait au milieu de la page | revient en haut |
| Zoom automatique iOS à chaque saisie | jusqu'à 58 champs | **0** |
| Réponses de QCM trop petites à viser | jusqu'à 100 % | **0** |
| Exercices de glisser-déposer au doigt | impossibles (2 exercices) | toucher pour choisir, toucher pour placer |

Ce qui a été mis en place :

- la barre du haut **se replie au défilement** : le titre et la ligne
  *Élève(s) : …* disparaissent vers le haut, seuls les onglets de niveau restent
  visibles (~46 px) ;
- les onglets tiennent **sur une seule ligne** et défilent horizontalement au doigt ;
- `scroll-padding-top` est calculé dynamiquement, donc les titres ne se cachent plus
  sous la barre ;
- le changement de niveau **remonte la page en haut** ;
- les exercices de glisser-déposer acceptent désormais le **toucher** (choisir puis placer),
  tout en conservant le glisser à la souris sur ordinateur ;
- les champs de saisie passent à **16 px** sur petit écran (seuil qui empêche iOS de zoomer) ;
- les réponses de QCM font au moins **44 px de haut**, la ligne entière étant cliquable.

Trois structures d'en-tête différentes coexistent dans les activités ; le correctif les
détecte automatiquement. Quand les onglets sont **dans** l'en-tête, celui-ci se replie jusqu'à
eux ; quand ils sont dans un `<nav>` **hors** de l'en-tête (activités « évolution des OST »,
« la souris », « choix des lampes »), l'en-tête disparaît entièrement et le `<nav>` se colle en
haut de l'écran.

Sur ordinateur, le rendu et le comportement sont **inchangés** (vérifié en 1280×900) : la barre
reste collante et les onglets reviennent à la ligne.

> Le correctif est appliqué par le script `_outils/appliquer_correctifs_mobile.py` du dossier de
> préparation : pour une nouvelle activité, le lancer sur le fichier avant de le copier ici.

### Pas d'export, pas d'impression

Il n'y a **volontairement plus** de bouton d'export PDF, de copie ou d'impression dans ces
pages : l'élève fait l'exercice, il ne rend rien (voir « Données et vie privée » ci-dessous).
Le générateur `_outils/gabarit/construire_activite.py` n'injecte plus ce module ; l'option
`--avec-export` existe encore, mais aucune page publiée ne l'utilise.

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

- **Aucune donnée personnelle n'est demandée aux élèves** : pas de champ nom, prénom
  ou binôme, pas de compte, pas de courriel, et **aucune ligne d'identification à
  remplir**. Ces activités sont des exercices à faire, pas des devoirs à rendre.
- Les activités **ne conservent rien** : ni sur un serveur, ni dans le navigateur de
  l'élève. Aucun export (PDF, texte, JSON), aucune copie dans le presse-papiers, aucune
  impression n'est proposé aux élèves : un élève qui revient refait l'exercice depuis le
  début, avec le même lien fourni par la messagerie.
- Aucun cookie, aucun traceur, aucune mesure d'audience n'est utilisé.
- Les liens vers les fiches, vidéos et quiz externes (Podeduc, Nuage, Google Forms) ne sont
  sollicités que si l'élève clique dessus ; ils nécessitent une connexion.

---

## Licence

MIT — voir [LICENSE](LICENSE).
