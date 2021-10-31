Change directory to */krypton/krypton6* and list its files:
```
krypton6@krypton:~$ cd /krypton/krypton6

krypton6@krypton:/krypton/krypton6$ ls
encrypt6  HINT1  HINT2  keyfile.dat  krypton7  onetime  README

krypton6@krypton:/krypton/krypton6$ file *
encrypt6:    setuid ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=36c96ef54e4786c48f84343d72fdc35cf85425e5, not stripped
HINT1:       ASCII text
HINT2:       ASCII text
keyfile.dat: regular file, no read permission
krypton7:    ASCII text, with no line terminators
onetime:     directory
README:      ASCII text
```

Read Hints:
```
krypton6@krypton:/krypton/krypton6$ cat HINT1
The 'random' generator has a limited number of bits, and is periodic.
Entropy analysis and a good look at the bytes in a hex editor will help.

There is a pattern!

krypton6@krypton:/krypton/krypton6$ cat HINT2
8 bit LFSR

```

HINT2 doesn't make sense to me at all, but HINT1 told us that random generator is periodic, so it is generating fixed size strings repeatedly.
At this point, we have the following information:
1. 'random' generator is periodic
2. Encryption algorithm works like this: takes one byte(one letter) from the plaintext and corresponds it to another byte(letter) from the key. Then it calculates XOR of their
   binary representations and converts it back to the letter. 
   For example: if the first letter of plaintext is A (01000001) and the first letter of the key is B(01000010), their XOR will be 00000011, which is equivalent of **L**.
                So the first letter of ciphertext will be L.
