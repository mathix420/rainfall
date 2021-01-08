1. On trouve un `memcpy` dans la méthode `setAnnotation`, on va donc utiliser cela pour exécuter un shellcode.
2. Pour trouver l'offset on utilise https://wiremask.eu/tools/buffer-overflow-pattern-generator/
   ```
   (gdb) r 'Aa0[...]Ag5Ag'

   Program received signal SIGSEGV, Segmentation fault.
   0x08048682 in main ()

   (gdb) info registers

   eax            0x41366441
   ```
   Soit un offset de 108.
3. On écrit donc l'exploit en python.

> Flag: f3f0004b6f364cb5a4147e9ef827fa922a4861408845c26b6971ad770d906728