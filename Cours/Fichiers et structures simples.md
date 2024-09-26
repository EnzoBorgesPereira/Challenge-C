# Le C - Fichiers et structures simples

## Fichiers

Les fonctions de manipulation de fichiers sont définies dans la librairie `stdio.h`.

### #Ouverture

Pour ouvrir un fichier, on utilise la fonction `fopen`. La fonction renvoie un pointeur de type `file` sur le fichier ouvert.

```c
FILE *fichier = fopen("chemin/vers/fichier", "mode");
```

Les modes d'ouverture cf. slide 4. Les plus courants sont :

- `"w+"` : écriture et lecture, crée le fichier s'il n'existe pas, **écrase** le contenu s'il existe.
- `"a+"` : écriture et lecture, crée le fichier s'il n'existe pas, **ajoute** le contenu à la fin s'il existe.

*Note* : Les droits d'accès sont semblables aux systèmes Unix.

### Vérification

Il est important de vérifier si l'ouverture du fichier s'est bien passée.

```c
if (fichier == NULL) {
    printf("Erreur lors de l'ouverture du fichier");
} else {
    printf("Fichier ouvert avec succès");
}
```

### Fermeture

Pour fermer un fichier, on utilise la fonction `fclose`.

```c
fclose(fichier);
```

**Attention** : Ne pas utiliser `fclose` sur un fichier non ouvert ou déjà fermé.

### Écriture

Pour écrire dans un fichier, il faut l'on ouvre avec un mode qui supporte l'écriture.

```c
FILE *fichier = fopen("chemin/vers/fichier", "w+");
```

On retrouve plusieurs fonctions d'écriture :

- `fputc` : écrit un caractère à la position courante du curseur.
- `fputs` : écrit une chaîne de caractères à la position courante du curseur.
- `fprintf` : écrit une chaîne de caractères formatée à la position courante du curseur.

*Note* : Par défaut, le curseur est positionné au début du fichier.

#### Écriture avec `fputc`

```c
FILE *fichier = fopen("chemin/vers/fichier", "w");
if (fichier != NULL) {
    fputc('H', fichier);
    fputc('e', fichier);
    fputc('l', fichier);
    fputc('l', fichier);
    fputc('o', fichier);
    fclose(fichier);
}
```

Ici, le fichier contiendra `Hello`.

#### Écriture avec `fputs`

```c
FILE *fichier = fopen("chemin/vers/fichier", "w");
if (fichier != NULL) {
    fputs("Hello", fichier);
    fclose(fichier);
}
```

Ici, le fichier contiendra `Hello`.

#### Écriture avec `fprintf`

```c
FILE *fichier = fopen("chemin/vers/fichier", "w");
if (fichier != NULL) {
    fprintf(fichier, "Hello, %d!", 42);
    fclose(fichier);
}
```

Ici, le fichier contiendra `Hello, 42!`.

#### Ajout d'une ligne à la fin du fichier

```c
FILE *fichier = fopen("chemin/vers/fichier", "a");
if (fichier != NULL) {
    fprintf(fichier, "Hello\n");
    fclose(fichier);
}
```

### Lecture

Pour lire dans un fichier, il faut l'on ouvre avec un mode qui supporte la lecture.

```c
FILE *fichier = fopen("chemin/vers/fichier", "r");
```

On retrouve plusieurs fonctions de lecture :

- `fgetc` : lit un caractère à la position courante du curseur.
- `fgets` : lit une chaîne de caractères à la position courante du curseur, jusqu'à la limite donnée ou un saut de ligne.
- `fscanf` : lit une chaîne de caractères formatée à la position courante du curseur.

*Note* : Par défaut, le curseur est positionné au début du fichier.

#### Lecture avec `fgetc`

Ici, le fichier contient `Hello`, on le lit caractère par caractère.

```c
FILE *fichier = fopen("chemin/vers/fichier", "r");
if (fichier != NULL) {
    char c;
    c = fgetc(f);
    printf("%c", c); // H
    c = fgetc(f);
    printf("%c", c); // e
    c = fgetc(f);
    printf("%c", c); // l
    c = fgetc(f);
    printf("%c", c); // l
    c = fgetc(f);
    printf("%c", c); // o
    fclose(f); 
}
```

#### Lecture EOF

*EOF : End Of File.* Il indique la fin du fichier.

On retrouve un caractère spécial `EOF` qui indique la fin du fichier.

```c
FILE *fichier = fopen("chemin/vers/fichier", "r");
if (fichier != NULL) {
    char c;
    while ((c = fgetc(f)) != EOF) {
        printf("%c", c);
    }
    fclose(f);
}
```

Ici, le fichier contient `Hello`, on le lit caractère par caractère. Quand on arrive à la fin du fichier, on sort de la boucle.

#### Lecture avec `fgets`

Quand `fgets` arrive à la fin du fichier, il renvoie `NULL`.

```c
FILE *fichier = fopen("chemin/vers/fichier", "r");
if (fichier != NULL) {
    char buffer[100] = {0};

    fgets(buffer, 100, f);
    printf("%s", buffer); // Hello, 1!

    fclose(f);
}
```

#### Lecture avec `fscanf`

```c
FILE *fichier = fopen("chemin/vers/fichier", "r");
if (fichier != NULL) {
    char buffer[100] = {0};
    int i;

    fscanf(f, "%s, %d!", buffer, &i);
    printf("%s, %d!", buffer, i); // Hello, 1!

    fscanf(f, "%s, %d!", buffer, &i);
    printf("%s, %d!", buffer, i); // Hello, 2!

    fclose(f);
}
```

### Déplacement du curseur

Plusieurs fonctions permettent de déplacer le curseur :

- `ftell` : renvoie la position du curseur.
- `fseek` : déplace le curseur à une position donnée.
- `rewind` : déplace le curseur au début du fichier (index 0).

**Attention** : On ne doit pas utiliser ces fonctions sur un fichier ouvert en mode `a`.

#### Déplacement du curseur avec `ftell`

Les fonctions de lecture et d'écriture déplacent le curseur automatiquement.

```c
FILE *fichier = fopen("chemin/vers/fichier", "r");
if (f != NULL)
{
    printf("%ld\n", ftell(f)); // 0
    fputc('a', f);
    printf("%ld\n", ftell(f)); // 1
    fputc('b', f);
    printf("%ld\n", ftell(f)); // 2
    fclose(f);
}
```

#### Déplacement du curseur avec `fseek`

La fonction `fseek` prend 2 arguments :

- Pointeur sur le fichier.
- Position du curseur.
- Origine du déplacement.

```c
FILE *fichier = fopen("chemin/vers/fichier", "r");
if (f != NULL)
{
    fseek(f, 2, SEEK_SET); // Déplace le curseur à la position 2
    printf("%ld\n", ftell(f)); // 2

    fseek(f, 2, SEEK_CUR); // Déplace le curseur de 2 positions, de la position courante
    printf("%ld\n", ftell(f)); // 4

    fseek(f, 0, SEEK_END); // Déplace le curseur à la fin du fichier
    printf("%ld\n", ftell(f)); // 6

    fclose(f);
}
```

Les origines possibles sont :

- `SEEK_SET` : début du fichier.
- `SEEK_CUR` : position courante.
- `SEEK_END` : fin du fichier.

## Les structures

Une structure est un type contenant un ensemble de propriétés.

### Déclaration

Pour déclarer une structure, on utilise le mot-clé `struct`.

```c
struct Student {
    char *firstname;
    char *lastname;
    int age;
};
```

Astuce : On peut simplifier l'affection des propriétés :

```c
struct Student
{
   char *firstname;
   char *lastname;
   int age;
};

int main()
{
   struct Student dennis = {
       .firstname = "Dennis",
       .lastname = "Ritchie",
       .age = 30,
   };
   return 0;
}
```

Il est possible de déclarer une structure dans l'odre de la déclaration des propriétés.

```c
struct Student
{
   char *firstname;
   char *lastname;
   int age;
};

int main()
{
   struct Student dennis = {"Dennis", "Ritchie", 30};
   return 0;
}
```

### Typedef

Pour simplifier l'utilisation d'une structure, on peut utiliser `typedef`.

```c
typedef struct Student
{
   char *firstname;
   char *lastname;
   int age;
} Student;

int main()
{
   Student dennis;
   return 0;
}
```

*Note* : Les variables non initialisées sont initialisées à la valeur par défaut du type.

### Utilisation

Pour accéder aux propriétés d'une structure, on utilise le `.`.

```c
typedef struct Student
{
   char *firstname;
   char *lastname;
   int age;
} Student;

int main()
{
   Student dennis = {"Dennis", "Ritchie", 30};
   printf("%s %s, a %d ans\n", dennis.firstname, dennis.lastname, dennis.age); // Dennis Ritchie, a 30 ans
   return 0;
}
```

### Tableaux

Il est possible de déclarer des tableaux de structures.

```c
typedef struct Student
{
   char *firstname;
   char *lastname;
   int age;
} Student;

int main()
{
   Student students[3] = {
       {"Dennis", "Ritchie", 30},
       {"Ken", "Thompson", 30},
       {"Linus", "Torvalds", 30},
   };

   for (int i = 0; i < 3; i++)
   {
       printf("%s %s, a %d ans\n", students[i].firstname, students[i].lastname, students[i].age);
   }
   return 0;
}
```

### Pointeurs

Il est possible de déclarer des pointeurs de structures, on utilise `->`.

```c
typedef struct Student
{
   char *firstname;
   char *lastname;
   int age;
} Student;

int main(){
    Student dennis = {"Dennis", "Ritchie", 30};

    Student *p = &dennis;
    printf("%s %s, a %d ans\n", p->firstname, p->lastname, p->age); // Dennis Ritchie, a 30 ans
    return 0;
}
```

### Usage avec les fonctions

Les structures peuvent être passées en argument à une fonction en tant que pointeur afin de le modifier, si on passe directement la structure, on ne peut pas la modifier.

```c
typedef struct Student
{
   char *firstname;
   char *lastname;
   int age;
} Student;

void increment_age(Student *student)
{
   student->age++;
}

int main()
{
   Student dennis = {"Dennis", "Ritchie", 30};
   increment_age(&dennis);
   printf("%s %s, a %d ans\n", dennis.firstname, dennis.lastname, dennis.age); // Dennis Ritchie, a 31 ans
   return 0;
}
```

### Allocation dynamique

Il est possible d'allouer dynamiquement une structure, on utilise `malloc`, **attention** à libérer la mémoire avec `free`.

```c
typedef struct Student
{
   char *firstname;
   char *lastname;
   int age;
} Student;

int main()
{
   Student *dennis = malloc(sizeof(Student));
   // ...
   free(dennis);

   return 0;
}
```
