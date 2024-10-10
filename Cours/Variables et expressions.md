# Le C - Variables et expressions

Créer en 1972 -> Dennis Ritchie et un des créateurs de UNIX

Langage compiler -> gcc / clang

## Types

int, char, string...

### Types de base

Les types ont une tailles différentes (en oct)
On peut connaitre la taille d'un type -> size_of
Les types peuvent être convertie de manière explicite ou implicite.

on déclarle le type puis le nom (int a = 1)

si on ne déclare pas de valeur, erreur -> il faut init la valeur dans tous les cas.

Scope : limite dans laquel on peut utiliser la variable (par block => dans un if, une méthode, une fonction...).

### Les nombres entier

Signé : pas négatif (on utilise tous les bit)
Non-signé : négatif ou possitif -> on perd un bit, car le premier déclare le signe

```c
unsigned int c = 1
```

#### Limites

char, short, int, long (cf. slide)
Il est possible de dépasser la limite d'espace d'un entier (overflow), utiliser le bon type pour éviter le pb.

#### Méthode de déclaration

On peut déclarer un entier de plusieurs manière

#### Boolean

Les bool sont 1 ou 0 et non true ou false.

#### Float

Ils sont sur 32bits, on déclare comme cela :

```c
3.14f;
```

#### Char

Déclaration avec 'a',
\n : saut de ligne
\t : tabulation
\0 : char Null

Si on fait '0' cela remonte 49, alors que \0 remonte 0 en tant que char.

## Opérateur

Expressions classiques :
+, -, *, /, %...

Manipulation de bit:

- ~ : Complément à un
- & : ET
- | : OU inclusif
- ^ : XOR / OU exclusif
- << : Décalage de bits vers la gauche ( a << 2 -> déclale de 2 vers la gauche)
- '>>' :  Décalage de bits vers la

## Fonction

printf : permet d'écrire dans la console (besoin d'import une biblio)
On peut écrire des char, des variables, des calculs...

On peut formater les éléments de sortie (taille de l'int ou du float)

Cf. Fonction printf -> slide 25.
