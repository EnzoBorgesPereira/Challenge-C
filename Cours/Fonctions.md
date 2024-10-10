# Le C - Fonctions

Une fonction est un bloc de code qui a un nom et qui peut être appelé depuis un autre endroit du programme.

## Déclaration d'une fonction

```c
type_retour nom_fonction(type_argument1 arg1, type_argument2 arg2, ...) {
    // Code de la fonction
}
```

Si une fonction ne retourne rien, on utilise `void` comme type de retour. Dans ce cas on peut omettre le `return`.

## Appel d'une fonction

```c
type_retour variable = nom_fonction(arg1, arg2, ...);
```

On déclare une fonction avant de l'appeler. Si la fonction est définie après l'appel, on utilise un prototype.

## Spécificité des arguments

Les arguments sont passés par valeur, c'est-à-dire que la fonction reçoit une copie de la valeur de l'argument.

cf. slide 8.

## Récursivité

Une fonction peut s'appeler elle-même. Il faut faire attention à ne pas créer de boucle infinie.

```c
//Fibonacci
int fibonacci(int n) {
    if (n <= 1) {
        return n;
    } else {
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
}
```

La limite ou "call stack", est incrémenter à chaque appel de fonction. Si la limite est atteinte, le programme crash.
