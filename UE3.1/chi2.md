# Institut Villebon Georges Charpak -- UE 3.1 Transmission de l'Information
## Travaux Pratiques: Test du X² (prononcé Chi 2)


En 1948 une étude sur l'alimentation des poulets a été publiée dans le journal Biometrika.

Dans cette expérience, un échantillon de 71 poulets a été nourri avec les six
types d'aliments suivants: _caséine_, _févérolles_, _lin_, _farine animale_,
_soja_ et _tournesol_. Puis après six mois, on a relevé le poids de chaque
poulet en grammes.

Dans cette séance de TP vous allez étudier ce jeu de données (tiré d'une étude scientifique réelle)
et en tirer des conclusions sur l'impact de l'alimentation sur la croissance des poulets.

Pour cela nous allons utiliser le test du $\chi^2$ pour répondre à la question: **Est-ce que l'alimentation
et le poids des poulets sont des variables indépendantes ?**

![Ferme de poulets en Floride (United States Department of Agriculture, image dans le domaine public)](Florida_chicken_house.jpg "Ferme de poulets en Floride (United States Department of Agriculture, image dans le domaine public)")

## Rappel: compilation et exécution de code C

Pour compiler un programme, on utilise un compilateur qui transforme un
ensemble de fichiers source (terminés par l'extension ```.c```) en un programme
exécutable.  L'année dernière vous avez utilisé le compilateur ```gcc```, cette
année nous vous proposons d'en utiliser un autre appellé ```clang```. Mais
rassurez vous, ```gcc``` et ```clang``` ont pratiquement la même interface
ligne de commande ! 

Par exemple pour compiler et executer le code ```test.c```, on fait les commandes suivantes:

```bash
$ clang -Wall test.c -o executable
$ ./executable
```

(@) Que fait l'option `Wall` ? 

## Lecture des données

Le fichier ```poulets.data``` contient le jeu de données déjà présenté.
Voici les 5 premières lignes du fichier:

```
71
179 1
160 1
136 1
227 1
...
```

La première ligne contient le nombre d'entrées, ici 71.  Puis lignes suivantes
correspondent au poids et à l'alimentation pour les 71 poulets participant à
l'expérience. La première colonne donne le poids en gramme, la deuxième colonne
donne l'alimentation (chiffre de 1, caséine, à 6, tournesol).

On souhaiterait connaître l'effectif de poulets pour chaque type d'aliments.
Par exemple, on voudrait savoir combien de poulets on été nourris avec des
farines animales.

(@) Ecrivez un programme qui donne l'effectif des poulets par type d'aliment. Pour cela il faudra 
lire les données depuis le fichier. Vous pouvez utiliser les fonctions de la libraire C suivantes:
```fopen```, ```fscanf```, ```fclose```.

## Discrétisation

Pour utiliser le test du $\chi^2$ il nous faut des variables discrètes. Or le
poids est une variable continue, il faut la discrétiser.

Pour cela nous allons classer les poulets en deux catégories de poids: les
poulets _légers_ (poids inférieur à 258 grammes) et les poulets _gros_ (poids
supérieur ou égal à 258 grammes). 

(@) Ecrivez un programme qui donne le nombre de poulets gros et de poulets petits.
Que remarquez vous ? Comment 258 a été choisi ?  

## Table croisée (ou table de contigence)

Maintenant on va appliquer la méthode du $\chi^2$. La première étape est de
générer la table de croisée des effectifs de poulets.

(@) Ecrivez un programme qui affiche la table croisée sous le format suivant:
```
                alimentation
          1   2   3   4   5   6 
    leger ?   ?   ?   ?   ?   ?
    gros  ?   ?   ?   ?   ?   ?
```

Bien entendu il faut remplacer les ```?``` par les effectifs de poulets dans
chaque catégorie (leger et caséine, leger et févérolles, etc.)

## Table croisée idéale en cas d'indépendance

La deuxième étape est de générer la table croisée idéale que l'on obtiendrai si
le poids et l'alimentation étaient indépendantes. 

Si les deux variables sont idépendantes, on peut appliquer la formule de Bayes
qui dit que si $A$ et $B$ sont independants alors $p(A \textrm{ et } B) = p(A)
\times p(B)$ où $p(A)$ est la probabilité de $A$.

Prennons un exemple pour trouver la case _leger et caséine_, 

$$p(\textrm{leger et caseine}) = p(\textrm{leger}) \times p(\textrm{caseine})$$ 

Ce qui peut être réecrit de la manière suivante,

$$\frac{\textrm{effectif legers et caseine }}{\textrm{effectif total}}  = \frac{\textrm{effectif de poulets legers}}{\textrm{effectif total}} \times  \frac{\textrm{effectif de poulets mangeant de la caseine}}{\textrm{effectif total}}$$

et donc

$$\textrm{effectif legers et caseine }  = \frac{\textrm{effectif de poulets legers} \times \textrm{effectif de poulets mangeant de la caseine}}{\textrm{effectif total}}$$

(@) Généralisez la formule et utilisez la pour générer la table croisée idéale en cas d'indépendance.

## Test du X²

Tout est prêt pour calculer le test du $\chi^2$ !

Il suffit pour cela d'appliquer la formule suivante:

$$\chi^2 = \sum_{i=1}^{n}\frac{(O_i-E_i)^2}{E_i}$$

où $n$ le nombre de cases du tableau, $O_i$ les valeurs du tableau généré en
question (4) et $E_i$ les valeurs du tableau générées en question (5). 

(@) Calculez la valeur du test pour l'expérience des poulets.

(@) Combien de degrées de liberté il y a dans cette expérience ?

(@) En utilisant la valeur du test, le nombre de degrées de liberté, et la table du $\chi^2$ qui vous a été distribuée, que pouvez vous conclure ?

## Questions pour approfondir

(@) Y a t'il des aliments plus efficaces que d'autres pour faire grossir les poulets? Si oui lequels ?

(@) Avec les données dont vous disposez peut on conclure qu'un des six types d'aliments est plus efficace que tous les autres ? Argumentez! 
