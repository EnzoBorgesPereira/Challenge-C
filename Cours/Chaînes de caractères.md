# Le C - Chaînes de caractères

Une chaîne de caractères est un tableau de caractères, on peut le stocker dans un tableau de caractères.

Une chaîne de caractères statique est mise dans un pointeur, elle est non modifiable, contraitement au format tableau :

```c
char string[] = "Hello"; // Chaîne de caractères modifiable
char *string = "Hello"; // Chaîne de caractères statique
```

On peut donner une taille à un tableau de caractères, mais il faut penser à ajouter un caractère pour le caractère de fin de chaîne `\0`.

```c
char string[6] = "hello";
char string[] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

## Manipulation de chaînes de caractères

Impossible d'utiliser les opérateurs `==` et `!=` pour comparer des chaînes de caractères. Il faut utiliser la fonction `strcmp` de la librairie `string.h`.

```c
#include <string.h>

char string1[] = "Hello";
char string2[] = "Hello";

if (strcmp(string1, string2) == 0) {
    // Les chaînes sont identiques
}
```

La fonction `strcmp` retourne un entier :

- `0` : Les chaînes sont identiques.
- `> 0` : La première chaîne est plus grande que la deuxième.
- `< 0` : La première chaîne est plus petite que la deuxième.

Pour copier une chaîne de caractères, on utilise la fonction `strcpy`.

```c
#include <string.h>

const char *source = "Hello";

char *destination = malloc(sizeof(char) * 10); // Allocation de mémoire pour destination

strcpy(destination, source); // Copie source dans destination

printf("%s\n", destination); // "Hello"
```

`strcpy` copie aussi le caractère de fin de chaîne `\0`.

On peut également utiliser `strcpy` pour limiter le nombre de caractères copiés.

La fonction `strcat` permet de concaténer deux chaînes de caractères.

```c
#include <string.h>

const char *a = "Hello";
const char *b = "World";

char *result = malloc(sizeof(char) + strlen(a) + strlen(b) + 1); // Allocation de mémoire pour result

strcpy(result, a); // Copie a dans result
strcat(result, b); // Concatène b à result

printf("%s\n", result); // "HelloWorld"
```

**Attention** : Il faut s'assurer d'avoir suffisamment de mémoire pour stocker les deux chaînes.

Pour connaître la longueur d'une chaîne de caractères, on utilise la fonction `strlen`. Renvoie un unsigned long.

```c
#include <string.h>

const char *a = "Hello";

printf("%lu\n", strlen(a)); // 5
```

### Réécriture de strlen

```c
#include <stdio.h>
#include <string.h>

unsigned long my_strlen(const char *str)
{
   unsigned long length = 0;

   while (*str != '\0')
   {
       length++;
       str++; // On passe au caractère suivantn en décalant le pointeur
   }
   return length;
}

int main()
{
   char str[] = "1234";

   printf("%lu", my_strlen(str)); // 4

   return 0;
}
```

## Table ASCII

Le tableau ASCII est un tableau de correspondance entre les caractères et les nombres. Chaque caractère est représenté par un nombre.

cf. slide 15.

Chaque caractère est représenté par un nombre, on peut donc effectuer des opérations sur les caractères.

```c
char c = 'A';

printf("%c\n", c); // A
printf("%c\n", c + 1); // B
```
