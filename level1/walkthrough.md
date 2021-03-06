1. Désassembler l'exécutable
   ```
   gdb level1
   set disassembly-flavor intel
   disas main
   ```
2. Peu d'infos donc on décide de lister les fonctions de l'exécutable
   ```
   info functions
   ```
3. On remarque la fonction `run`
   ```
   ┌ 60: sym.run ();
   │           ; var size_t size @ esp+0x4
   │           ; var size_t nitems @ esp+0x8
   │           ; var FILE *stream @ esp+0xc
   │           0x08048444      55             push ebp
   │           0x08048445      89e5           mov ebp, esp
   │           0x08048447      83ec18         sub esp, 0x18
   │           0x0804844a      a1c0970408     mov eax, dword [obj.stdout] ; obj.stdout__GLIBC_2.0
   │                                                                      ; [0x80497c0:4]=0
   │           0x0804844f      89c2           mov edx, eax
   │           0x08048451      b870850408     mov eax, str.Good..._Wait_what__n ; 0x8048570 ; "Good... Wait what?\n"
   │           0x08048456      8954240c       mov dword [stream], edx     ; FILE *stream
   │           0x0804845a      c74424081300.  mov dword [nitems], 0x13    ; [0x13:4]=-1 ; 19 ; size_t nitems
   │           0x08048462      c74424040100.  mov dword [size], 1         ; size_t size
   │           0x0804846a      890424         mov dword [esp], eax        ; const void *ptr
   │           0x0804846d      e8defeffff     call sym.imp.fwrite         ; size_t fwrite(const void *ptr, size_t size, size_t nitems, FILE *stream)
   │           0x08048472      c70424848504.  mov dword [esp], str._bin_sh ; [0x8048584:4]=0x6e69622f ; "/bin/sh" ; const char *string
   │           0x08048479      e8e2feffff     call sym.imp.system         ; int system(const char *string)
   │           0x0804847e      c9             leave
   └           0x0804847f      c3             ret
   ```
4. Notre but sera donc de faire un buffer overflow sur le `gets` de la fonction `main` afin d'exécuter la fonction `run` à l'adresse `0x08048444`
5. On écrit un exploit (`exploit.py`)

> Flag: 53a4a712787f40ec66c3c26c1f4b164dcad5552b038bb0addd69bf5bf6fa8e77