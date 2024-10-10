# Le C - Tableaux

Un tableau est un ensemble d'éléments de même type, indexé par un entier.

Déclaration d'un tableau :

```c
type name[size];

int tab[5];
```

La taille du tableau est fixe, impossible de changer avec ce type de déclaration.

On peut initialiser un tableau de plusieurs manières :

```c
int tab[5] = {1, 2, 3}; // Les éléments 4 et 5 sont à 0
int tab[5] = {0}; // Tous les éléments sont à 0
```

## Liste d'initialisation

```c
int tab[] = {1, 2, 3}; // La taille est déduite du nombre d'éléments
```

## Accès aux éléments

```c
int grade[5] = {1, 2, 3, 4, 5};

int frist = grade[0]; // 1er élément
int last = grade[4]; // 5ème élément

printf("%d\n", grade[2]); // 3ème élément
```

On essaye d'accéder à un élément qui en dehors du tableau (exemple : `grade[5]`), cela déclenche une erreur de ségmentation.

## Affectation d'éléments

```c
int grade[5];
grade[0] = 1; // 1er élément = 1
```

## Parcours d'un tableau

```c
int grade[5] = {1, 2, 3, 4, 5};

for (int i = 0; i < 5; i++) {
    printf("Grade %d: %d\n", i, grade[i]);
}
```

En C il n'y a pas de ```.lenght``` comme en JS, il faut donc connaître la taille du tableau pour le parcourir.

Attention la capacité de stockage d'un tableau est limitée, il est possible de dépasser cette limite et d'écraser des données.

Pour parcourir un tableau, il est possible de déclarer une variable pour connaître le nombre d'éléments du tableau.

## Tableau multidimensionnel

```c
int tab[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};

int tab[2][3] = {0}; // Tous les éléments sont à 0

//La taille n'est pas nécessaire, elle est déduite du nombre d'éléments (UNIQUEMENTD pour les lignes, non recommandé)
int tab[][3] = {
    {1, 2, 3},
    {4, 5, 6}
};
```

Celui-ci est un tableau de 2 lignes et 3 colonnes, semblable à une matrice.

### Accès aux éléments dans un tableau multidimensionnel

Nous pouvons accéder aux éléments de la manière suivante :

```c
int tab[2][3] = {0};

tab[0][0] = 1; // 1ère ligne, 1ère colonne
tab[1][2] = 6; // 2ème ligne, 3ème colonne
```

### Exemple : table de multiplication

```c
int mult[10][10];

// Remplissage de la table de multiplication
for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 10; j++) {
        mult[i][j] = i * j;
    }
}

// Affichage de la table de multiplication
for (int i = 0; i < 10; i++) {
    for (int j = 0; j < 10; j++) {
        printf("%d * %d = %d\n", i, j, mult[i][j]);
    }
}
```

#### Tips exercice

Dans les exercices, on vas trouver ``` ** ```, cela signifie que l'on a un tableau de tableau.
