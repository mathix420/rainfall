1. En procédant par étapes j'ai en premier lieu désassemblé le programme `level0` afin d'en comprendre son fonctionnement
2. J'ai trouvé ce bloc intéressant
   ```
   call   0x8049710 <atoi>
   cmp    eax,0x1a7
   jne    0x8048f58 <main+152>
   ```
3. Il suffit donc de donner la valeur `0x1a7` en entrée, soit `423`
4. En faisant cela un shell apparaît, il suffit de taper la commande suivante pour obtenir le flag
   ```
   cat /home/user/level1/.pass
   ```

> Flag: 1fe8a524fa4bec01ca4ea2a869af2a02260d4a7d5fe7e7c24d8617e6dca12d3a
