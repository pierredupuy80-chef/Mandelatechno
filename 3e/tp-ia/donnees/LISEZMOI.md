# Les données des ateliers d'IA (3<sup>e</sup>)

Ce dossier contient les données de **deux ateliers** :

- **`atelier_ia_exemples.json`** — l'atelier **« L'IA apprend avec des exemples »**
  (`atelier-ia-exemples.html`, celui à utiliser en classe) : les chiffres, les images et les sons.
  Voir la section ci-dessous.
- **les 6 fichiers `.csv`** — la **version longue** (`tp-ia.html`, voir `GUIDE-version-longue.md`) :
  le volet à lames orientables, les mesures sur 24 h et les tables de récompenses.

Ces fichiers sont **déjà embarqués dans la page correspondante** : ils ne sont pas nécessaires pour
faire les ateliers. Ils servent à trois choses :

1. **montrer les données brutes** aux élèves (les ouvrir dans un tableur) ;
2. **les modifier** et réimporter le fichier modifié dans la page (boutons *Importer un CSV*) ;
3. **refaire les calculs** à la main ou dans un tableur (statistiques, graphiques).

Format : texte **UTF-8**, séparateur **point-virgule** (`;`), premières lignes en commentaire
(elles commencent par `#` et sont ignorées à l'import), **virgule ou point** acceptés pour les
décimales. Un tableur français (LibreOffice Calc, Excel) ouvre ces fichiers directement par
double-clic.

## `atelier_ia_exemples.json` — les données de l'atelier « Comment les IA apprennent-elles ? »

Utilisé par `atelier-ia-exemples.html`. Ce fichier contient **tout** ce dont la page a besoin :

| Clé | Onglet | Contenu |
|---|---|---|
| `chiffres` | 1. Supervisé | 10 exemples de « 3 » et de « 8 » (5 par famille), 10 images de test (série A), 10 images jamais montrées (série B), et `controle` : tous les scores attendus |
| `modes.nonSupervise` | 4. Non supervisé | 12 images de chiffres **sans aucune étiquette** (`images`, `familles`), les paquets trouvés par l'IA (`groupes`), leur taille (`repartition`) et leur propreté (`purete`) |
| `modes.visages` | 4. Non supervisé | les **visages** : `personnes` (3 identités : teinte, cheveux, coiffure, mesures du visage) · `photos` (12 photos : la personne, la pose, la lumière, les lunettes, le chapeau, et les mesures que l'IA en tire) · `mesures` (la liste affichée aux élèves) · `paquets` (le paquet de chaque photo) · `repartition`, `proprete` · `erreurs` (la photo mal rangée) · `dure` |
| `modes.autoSupervise` | 2. Auto-supervisé | `types` (les 5 genres, nom + emoji) · `colonnes` × `bandes` (la taille du dessin) · `exemples` (5 sons de la **mémoire**, avec `modele` = le dessin et `son` = l'extrait audio) · `sons` (les 5 sons à deviner : `vraie`, `devinee`, `cache`, `bien`, `sonores`, `differentes`, `son`, `fichier_test`) · `total10` · `credits` |

Comment lire les données :

- **une image** : une suite de `0` (case blanche) et de `1` (case noire), ligne par ligne, sur une
  grille de 11 × 11 ;
- **un son** : une suite de 18 nombres entre 0 et 1 (la hauteur des barres) ;
- **une case d'échecs** : `[colonne, ligne]`, la colonne 0 est le côté « a » et la ligne 0 est le haut
  de l'échiquier (la rangée 8) ;
- **un visage** : les traits dessinés (largeur, hauteur, écart des yeux, largeur de la bouche) et les
  traits de la photo (pose, lumière, lunettes, chapeau). L'IA en tire 6 **mesures** (clarté de la peau,
  largeur et hauteur du visage, écart des yeux, largeur de la bouche, couleur des cheveux) : c'est sur
  ces mesures — et non sur les personnes — que se font les paquets. La photo n° 8 est celle qui trompe
  l'IA : prise en plein soleil avec un chapeau clair, ses cheveux noirs sont cachés, et sa couleur de
  cheveux mesurée ressemble à celle de la personne A.

Dans `chiffres.controle` : `avantA`, `ratees`, `apresA`, `avantB`, `apresB` (sans donnée biaisée),
`poison_position`, `poison_score` (série A avec la donnée mal étiquetée) et `poisonB` (série B avec la
donnée mal étiquetée).

Ces données ne sont pas choisies au hasard : le programme de génération fabrique des candidats puis
**sélectionne** ceux qui donnent une démonstration nette — l'IA se trompe au départ, réussit après
l'aide, progresse sur des cas jamais vus, un seul mauvais exemple fait chuter le score, et avec
beaucoup moins d'exemples elle devine nettement moins bien. Les chiffres obtenus sont dans
`_outils/rapport_donnees_atelier_ia.txt` et `_outils/rapport_verification_atelier_ia.txt`.

---

## `volet_entrainement.csv` — 48 situations **étiquetées** (atelier 1)

| Colonne | Sens |
|---|---|
| `id` | numéro de la situation (`E01`…`E45`, `F01`…`F03`) |
| `luminosite_lux` | luminosité extérieure mesurée, en lux (0 → 95 000) |
| `temperature_C` | température, en °C (6 → 36) |
| `decision_utilisateur` | ce que l'utilisateur a fait : `fermer` ou `ouvrir` |

Points remarquables, à connaître pour guider les élèves :

- `F01` (9 000 lux / 24,0 °C → **fermer**), `F02` (20 000 lux / 21,0 °C → **fermer**) et
  `F03` (50 800 lux / 26,0 °C → **ouvrir**) sont des **erreurs d'étiquetage volontaires** : trois
  situations où l'utilisateur a cliqué sur la mauvaise réponse. Ce sont elles qui créent les
  « îlots » visibles à k = 1 et qui expliquent l'écart de réussite entre k = 1 (75 %) et k = 5 (90 %).
- Deux autres exemples de la zone tiède et lumineuse se contredisent presque (`E18`, `E20`…) :
  l'utilisateur n'y est pas constant. C'est volontaire : **100 % de réussite est impossible**.

## `volet_test.csv` — 20 situations **étiquetées**, jamais utilisées pour l'apprentissage

Mêmes colonnes. Sert uniquement à mesurer la réussite. Deux lignes sont à signaler :

- `Y01` (22 150 lux / 25,5 °C → ouvrir) et `Y02` (22 550 lux / 25,6 °C → fermer) : **deux situations
  quasi identiques étiquetées différemment**. Aucun modèle ne peut avoir raison sur les deux : la
  réussite parfaite est donc mathématiquement impossible, quel que soit le réglage.
- `Y03`, `Y04`, `Y05` sont posées juste à côté des erreurs d'étiquetage `F01`, `F02`, `F03` : k = 1 se
  trompe, k = 5 a raison. C'est la démonstration la plus nette de l'atelier 1.

## `volet_entrainement_desequilibre.csv` — 30 situations, **toutes « fermer »** (démonstration du biais)

Journal d'une semaine de canicule : le soleil tape, l'utilisateur a toujours fermé. Entraînée
là-dessus, l'IA répond « fermer » à **toutes** les situations, y compris une nuit douce, et sa
réussite sur les 20 tests tombe à **30 %**. Fichier à charger avec le bouton *« Données canicule »*.

## `volet_mesures_24h.csv` — 74 mesures, **aucune étiquette** (atelier 2)

| Colonne | Sens |
|---|---|
| `id` | `M01`…`M74` |
| `heure` | heure de la mesure (`00h00` → `23h40`, toutes les 20 minutes) |
| `luminosite_lux`, `temperature_C` | les deux grandeurs mesurées par les capteurs du volet |

`M73` (14h20, 900 lux, 27,5 °C) et `M74` (15h00, 1 200 lux, 28,4 °C) sont un **orage** : il fait
sombre *et* chaud. Les élèves doivent chercher où l'IA range ces deux mesures (réponse : avec les
mesures tièdes de la journée, à cause de la température — l'IA ne connaît pas la notion d'orage).

## `recompenses_confort.csv` et `recompenses_energie.csv` (atelier 3)

| Colonne | Sens |
|---|---|
| `etat` | la situation : `Soleil 32 °C`, `Nuageux 20 °C`, `Nuit`, `Orage 27 °C` |
| `ouvrir`, `fermer`, `laisser` | la note de 0 à 10 (satisfaction de l'utilisateur) pour chaque action |

Ces deux tables décrivent **le même système avec deux objectifs différents** ; l'agent ne les connaît
pas au départ, il les découvre par essais. Les modifier (dans un tableur) puis les importer avec le
bouton *« Importer un CSV de récompenses »* permet de fabriquer un objectif absurde et de constater
que l'IA apprend… exactement ce qu'on lui a demandé.

---

## Régénérer les fichiers

```bash
python3 _outils/generer_donnees_tp_ia.py   # déterministe : mêmes fichiers à chaque exécution
python3 _outils/construire_tp_ia.py        # réinjecte les données dans tp-ia.html
```

Les bornes, les règles et les cas particuliers sont lisibles et commentés dans
`_outils/generer_donnees_tp_ia.py` : c'est là qu'on modifie une valeur si l'on veut adapter le TP.
