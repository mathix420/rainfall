1. La vulnérabilité est encore strcpy, cette fois on doit l'utiliser pour exécuter la fonction `m` afin d'afficher la chaîne `c` précédemment lue dans le fichier `.pass` du level9.
2. En affichant la heap grâce à gdb (`x/32wx 0x804a000`) on comprend qu'en overridant le 6e octet on peut changer l'adresse d'écriture du second `strcpy`.
3. On choisit donc d'override l'adresse de puts dans la `GOT` afin de lancer la fonction `m` à la place.

> Flag: 5684af5cb4c8679958be4abe6373147ab52d95768e047820bf382e44fa8d8fb9
