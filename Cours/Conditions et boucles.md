# Le C - Conditions et boucles

## Opérateurs

### Relationnels

```string
> : Inférieur à
< : Supérieur à
<= : Inférieur ou égal à
>= : Supérieur ou égal à
== : Égal à
!= : Différent de
```

### Logiques

```string
&& : ET
|| : OU
! : NON
```

On note qu'il n'y a pas de true ou false en C, mais 0 pour faux et 1 pour vrai.

### If, else et else if

```c
if (condition) {
    // Code si condition vraie
} else if (autre_condition) {
    // Code si autre_condition vraie
} else {
    // Code si aucune condition vraie
}
```

### Switch

```c
switch (variable) {
    case valeur1:
        // Code si variable == valeur1
        break;
    case valeur2:
        // Code si variable == valeur2
        break;
    case valeur3:
    case valeur4:
        // Code si variable == valeur3 ou variable == valeur4
        break;
    default:
        // Code si aucune valeur ne correspond
        break;
}
```

L'absence de break permet de passer d'un case à l'autre.

### Ternaire

```c
int result = condition ? valeur_si_vrai : valeur_si_faux;
```

## Boucles

### While

```c
while (condition) {
    // Code tant que condition vraie
}
```

### For

```c
for (initialisation; condition; incrémentation) {
    // Code tant que condition vraie
}
```

### Do while

```c
do {
    // Code tant que condition vraie
} while (condition);
```

### Break et continue

```c
while (1) {
    if (condition) {
        break; // Sort de la boucle parente
    }
    if (autre_condition) {
        continue; // Passe à l'itération suivante
    }
}
```
