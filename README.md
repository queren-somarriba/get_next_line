# Get Next Line

Get Next Line (GNL) est une fonction en C permettant de lire une ligne d'un fichier, d'un flux d'entrée ou d'un socket de manière efficace.

## Installation

Pour compiler `get_next_line.c` et `get_next_line_utils.c`, utilisez la commande suivante :

```sh
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c -o gnl
```

Vous pouvez ajuster `BUFFER_SIZE` en fonction de vos besoins pour optimiser les performances.

## Utilisation

Dans votre projet, incluez le fichier d'en-tête de la bibliothèque :

```c
#include "get_next_line.h"
```

Exemple d'utilisation de `get_next_line` :

```c
#include <fcntl.h>
#include <stdio.h>
#include "get_next_line.h"

int main(void)
{
    int fd = open("file.txt", O_RDONLY);
    char *line;
    
    if (fd < 0)
        return (1);
    while ((line = get_next_line(fd)))
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

## Fonctionnalités

- Lecture d'un fichier ligne par ligne sans surcharge de mémoire
- Utilisation d'un buffer pour optimiser la lecture

## Fonctions implémentées

- `get_next_line` : Lit une ligne depuis un descripteur de fichier donné
- `get_next_line_utils.c` : Contient des fonctions utilitaires comme `ft_strlen`, `ft_strjoin`, et `ft_strchr`

## Bonus : Gestion de plusieurs fichiers simultanément

La version bonus de `get_next_line` permet la lecture simultanée de plusieurs fichiers en gérant chaque descripteur indépendamment.

### Fonctionnalités supplémentaires du bonus :
- Support de plusieurs descripteurs de fichiers en même temps.
- Stockage des données de lecture dans des buffers distincts pour chaque fichier ouvert.

### Exemple d'utilisation du bonus :

```c
#include <fcntl.h>
#include <stdio.h>
#include "get_next_line.h"

int main(void)
{
    int fd1 = open("file1.txt", O_RDONLY);
    int fd2 = open("file2.txt", O_RDONLY);
    char *line1;
    char *line2;
    
    if (fd1 < 0 || fd2 < 0)
        return (1);
    while ((line1 = get_next_line(fd1)) || (line2 = get_next_line(fd2)))
    {
        if (line1)
        {
            printf("File1: %s", line1);
            free(line1);
        }
        if (line2)
        {
            printf("File2: %s", line2);
            free(line2);
        }
    }
    close(fd1);
    close(fd2);
    return (0);
}
```

Projet développé dans le cadre du cursus 42.
