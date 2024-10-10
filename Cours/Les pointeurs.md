# Le C - Les pointeurs et allocation dynamique

Un pointeur est une référence à une adresse mémoire. Il permet de manipuler directement la mémoire.
Il est comme l'index d'un tableau mais dans la RAM.

## Représentation des pointeurs

Les éléments d'un tableau sont stockés de manière contiguë en mémoire, il est donc possible de les parcourir en utilisant des pointeurs.

Ici, on déclare un tableau de 5 entiers et on crée un pointeur qui pointe sur le premier élément du tableau.

```c
int tab[5] = {1, 2, 3, 4, 5};
```

## Opérateurs

- &a : référencement - récupère l'adresse de la variable
- *a : déréférencement - pointe vers la valeur à l'emplacemen du pointeur

Attention ``` & ``` fonctionne que sur les variables et les fonctions. Ne fonctionne pas sur les expressions.

```c
int a = 0;

int *b = &a;        // b pointe sur a (* indique que b est un pointeur)
int *c = &5         // erreur, on ne peut pas récupérer l'adresse d'une expression
int *d = &(a + a)   // erreur, on ne peut pas récupérer l'adresse d'une expression (même si a est une variable)
```

Avec ``` * ``` et ``` & ```, on peut passer de pointeur à valeur et de valeur à pointeur.

```c
int a = 0;

int *pointer_to_a = &a; // pointer_to_a pointe sur a
int value_of_a = *pointer_to_a; // value_of_a = 0
```

On peut aussi modifier la valeur de la variable à travers le pointeur.

```c
int a = 0;

int *pointer_to_a = &a; // pointer_to_a pointe sur a
*pointer_to_a = 1; // a = 1
```

## Type

Tout comme les tableaux, les pointeurs ont un type. Il est important de respecter le type du pointeur pour éviter des erreurs.

```c
type *my_pointer;
```

## Adresses

### Affichage

Pour afficher une adresse, on utilise le format ``` %p ```.

```c
int a = 0;
printf("%p\n", &a); // Affiche l'adresse de a
```

Une adresse est un nombre hexadécimal et sera toujours de la même taille.

### Arithmétique

On peut effectuer des opérations arithmétiques sur les pointeurs.

```c
int a = 0;

int *pointer_to_a = &a;
int *next = pointer_to_a + 1; // next pointe sur l'adresse suivante

printf("%p\n", pointer_to_a); // Affiche l'adresse de a
printf("%p\n", next); // Affiche l'adresse de a + 1
```

On décale le pointeur de la taille du type pointé, ici de 4 octets (int).

- Char : 1 octet
- Int / Float : 4 octets
- Long / Double : 8 octets
- Long double : 16 octets

**Attention** : lors de la manipulation des pointeurs, il faut être sûr de pouvoir accéder à l’emplacement mémoire ciblé lors d’un déréférencement sous risque de faire crasher le programme.

## Tableux et pointeurs

Les tableaux sont très proches des pointeurs.

```c
int tab[5] = {1, 2, 3};

printf("%d\n", tab); // Affiche l'adresse du premier élément
printf("%d\n", tab + 1); // Affiche l'adresse du deuxième élément
```

**Attention** : On peut transformer un tableau en pointeur mais pas l’inverse.

Pour accéder à un élément d'un tableau :

```c
int tab[5] = {1, 2, 3};
int *p = tab;

printf("%d\n", *p); // Affiche le premier élément
printf("%d\n", *(p + 1)); // Affiche le deuxième élément
```

*Astuce* : on peut utiliser ``` tab[i] ``` à la place de ``` *(tab + i) ```.

```c
int tab[5] = {1, 2, 3};
int *p = tab;

printf("%d\n", tab[0] == p[1]); // Affiche le premier élément
printf("%d\n", *(p+1) == p[1]); // Affiche le premier élément
```

## En entrée de fonction

Les pointeurs sont souvent utilisés pour passer des arguments à une fonction, cela évite la copie de la variable.

```c
void increment(int a) {
    a++;
}

int main(){
    int a = 0;
    increment(a);

    printf("%d\n", a); // Affiche 0
}
```

```c
void increment(int *a){
    *a++;
}

int main(){
    int a = 0;
    increment(&a);

    printf("%d\n", a); // Affiche 1
}
```

## En sortie de fonction

Ne JAMAIS retourner un pointeur vers une variable locale. Seul la mémoires allouée manuellement peut être retournée.

```c
int *get_pointer_bad()
{
   int a = 15;
   return &a; // NOOOOO
}

int *get_pointer_good(int *ptr)
{
   return ptr; // ok
}

int *get_pointer_good2()
{
   int *a = malloc(sizeof(int)); // allocation de 4 octets (taille d'un int)
   return a; // ok
}
```

``` malloc ``` permet d'allouer de la mémoire dynamiquement. Il faut penser à libérer la mémoire avec ``` free ```.

## Allocation dynamique

L’allocation dynamique est le principe d’allouer manuellement de la mémoire en fonction des besoins du programme.

### Bases

Une allocation dynamique permet de réserver de la mémoire à l'exécution du programme, avec ``` malloc ```.

Ici on alloue 5 entier, on utilise ``` sizeof ``` pour obtenir la taille d'un entier.

```c
int *tab = malloc(sizeof(int) * 5); // 5 entiers, soit 20 octets
```

Une fois l'accomplissement terminé, il faut libérer la mémoire avec ``` free ```.

```c
int *tab = malloc(sizeof(int) * 5);

*tab = 1;
*(tab + 1) = 2;
*(tab + 2) = 3;

printf("%d\n", *tab); // Affiche 1

free(tab); // Libère la mémoire allouée à tab
```

**Attention** : Seul la mémoire allouée dynamiquement doit être passée à ``` free ```.

Par défaut toutes les valeurs d'un pointeur sont inconnues. On utilise ``` calloc ``` pour initialiser les valeurs à 0.

```c
int *tab = calloc(5, sizeof(int)); // 5 entiers initialisés à 0

for (int i = 0; i < 5; i++) {
    printf("%d\n", *(tab + i)); // Affiche 0
}

free(tab);
```

### Pointeur "NULL"

Un pointeur qui n'a aucune valeur doit être initialisé à ``` NULL ```, qui est une constante égale à 0.

```c
int *tab = NULL;
````

On peut comparer un pointeur à ``` NULL ``` dans une condition.

```c
int *tab = NULL;

if (tab == NULL) {
    printf("tab est NULL\n");
}
```

### Tableaux

#### Problème

Jusqu'à présent on devions fournir la taille du tableau à sa déclaration.

```c
int grades[5] = {0};

int i = 0;
while (1)
{
    int grade;
    printf("Grade %d: ", i + 1);
    scanf("%d", &grade);

    if (grade == -1)
    {
        break;
    }

    grades[i] = grade; // Si i > 4, on dépasse la taille du tableau.
    i++;
}
```

#### Solution

##### Allocation dynamique d'un tableau

En C, on peut allouer un tableau dynamiquement en utilisant la fonction `malloc`. Cela permet de réserver de la mémoire pendant l'exécution du programme, en fonction des besoins.

```c
int *new_array(int size) {
    return malloc(size * sizeof(int));
}
```

##### Copier les éléments d'un tableau dans un autre

Lorsqu'on agrandit un tableau, il est nécessaire de copier les éléments de l'ancien tableau vers un nouveau plus grand :

```c
void copy_array(int *dest, int *src, int size) {
    for (int i = 0; i < size; i++) {
        dest[i] = src[i];
    }
}
```

##### Gestion de la capacité dynamique

L'idée est de commencer avec une capacité fixe, et lorsqu'elle est dépassée, doubler cette capacité :

```c
int main() {
    int capacity = 16;
    int *grades = new_array(capacity);
    int i = 0;

    while (1) {
        int grade;
        printf("Entrez une note (-1 pour arrêter) : ");
        scanf("%d", &grade);

        if (grade == -1) break;

        if (i == capacity) {
            capacity *= 2;
            int *tmp = new_array(capacity);
            copy_array(tmp, grades, i); // Redimensionne le tableau
            free(grades);
            grades = tmp;
        }

        grades[i] = grade;
        i++;
    }

    free(grades);
    return 0;
}
```

#### Solution ++

On peut utiliser la fonction ``` realloc ``` qui s’occupe du redimensionnement et de la copie des données du pointeur en plus de quelques optimisations.

```c
int main()
{
   int capacity = 16;
   int *grades = malloc(sizeof(int) * capacity);

   int i = 0;
   while (1)
   {
       int grade;
       printf("Grade %d: ", i + 1);
       scanf("%d", &grade);

       if (grade == -1)
       {
           break;
       }

       if (i == capacity)
       {
           capacity *= 2;
           grades = realloc(grades, sizeof(int) * capacity); // Redimensionne le tableau 
       }

       grades[i] = grade;
       i++;
   }

   free(grades);

   return 0;
}
````
