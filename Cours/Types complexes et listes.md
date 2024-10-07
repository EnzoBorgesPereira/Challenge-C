# Le C - Types complexes et listes

[Slide cours](https://docs.google.com/presentation/d/1frI7wmmifVi27A1EK5kEKkzD6oKGGDyefnyFORDpndQ/edit)

## Listes chaînées

Une liste chaînée est une structure de données pour agrandir dynamiquement la mémoire au fur et à mesure que les éléments sont ajoutés. Chaque élément de la liste est un nœud qui contient un élément de données et un pointeur vers le nœud suivant.

### Exemple

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

Node *ll_push_front(Node *head, int data) {
    Node *new = (Node *)malloc(sizeof(Node));
    new->data = data;
    new->next = head;
    return new;
}

void ll_free(Node *first)
{
   if (first != NULL)
   {
       ll_free(first->next);
       free(first);
   }
}

void ll_print(Node *first)
{
   while (first != NULL)
   {
       printf("%d", first->data);
       first = first->next;

       if (first != NULL)
       {
           printf(", ");
       }
   }
}

int main()
{
   Node *students = NULL;
   students = ll_push_front(students, 1);
   students = ll_push_front(students, 2);

   ll_print(students); // 2, 1
   ll_free(students);

   return 0;
}
```

## Enumérations

Une énumération permet de un nom à des entiers. Par exemple, pour les jours de la semaine.

### Déclaration

On ajoute le mot-clé `enum` suivi du nom de l'énumération et des valeurs entre accolades.

```c
enum Weekday {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
};
```

### Typedef

On peut utiliser `typedef` pour définir un alias pour l'énumération.

```c
typedef enum {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
} Weekday;
```
