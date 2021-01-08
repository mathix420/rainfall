1. Le but est assez clair, accéder au call `system("/bin/sh")`
2. On remarque également la mauvaise utilisation de `printf` qui est vulnérable
3. Notre but est donc d'override la valeur de l'objet `m (ds:0x804988c)`
4. L'option `%n` de printf peut nous aider à écrire à une adresse précise
5. Il faut maintenant trouver l'adresse de notre objet sur la stack afin d'écrire dessus
6. En essayant de lire le contenu de la stack afin d'y trouver notre adresse on s'apperçoit qu'un pattern apparaît
   ```
   python -c 'print "%x " * 1000' | ./level3

   [...] 78252078 20782520 25207825 [...]
   ```
7. En les décodant on remarque que c'est simplement les paramètres de printf que l'on vient d'écrire
   ```
   python -c 'print "20782520".decode("hex")'

   " x% "
   ```
8. Il suffit donc de mettre l'adresse désirée dans l'entrée afin de la voir apparaître sur la stack
9. En écrivant le payload on trouve l'adresse désirée à la 5e position
10. Maintenant en utilisant l'argument `%n` on peut override le contenu de l'adresse.
11. En trouvant le bon padding on arrive à override `m` avec `0x40`

```
(/tmp/exp.py; echo "cat /home/user/level4/.pass") | ./level3
```

> Flag: b209ea91ad69ef36f2cf0fcbbc24c739fd10464cf545b20bea8572ebdc3c36fa