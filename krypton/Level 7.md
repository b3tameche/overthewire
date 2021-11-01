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
Read our cipher:
```
krypton6@krypton:/krypton/krypton6$ cat krypton7
PNUKLYLWRQKGKBE
```
HINT1 told us that random generator is periodic, so it is generating fixed size strings repeatedly.
At this point, we have the following information:
1. 'random' generator is periodic
2. Encryption algorithm works like this: takes one one letter from the plaintext and corresponds it to another letter from the key. Then it calculates XOR of their
   binary representations and converts it back to the letter. 

Just like in Level 3, we're gonna create temporary directory as our workspace and make a symbolic link to keyfile:
```
krypton6@krypton:/krypton/krypton6$ mktemp -d
/tmp/tmp.J1EBWzVpoy
krypton6@krypton:/krypton/krypton6$ cd /tmp/tmp.J1EBWzVpoy
krypton6@krypton:/tmp/tmp.J1EBWzVpoy$ ln -s /krypton/krypton6/keyfile.dat
krypton6@krypton:/tmp/tmp.J1EBWzVpoy$ chmod 777 .
```

At first, I thought it would be helpful to create a file containing only characters with binary value of 01000000 (@), because its XOR with any letter would be
**chr(64 + XOR)** which would be actual key, but encryption didn't work on it (idk why).
I thought algorythm was only encrypting files with letters in it (ascii value in range of 65-90), so I created file with bunch of 'A's (since I didn't know 
random key length) and encrypted it.
```
krypton6@krypton:/tmp/tmp.J1EBWzVpoy$ vim test
krypton6@krypton:/tmp/tmp.J1EBWzVpoy$ cat test
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
krypton6@krypton:/tmp/tmp.J1EBWzVpoy$ /krypton/krypton6/encrypt6 test ciph
krypton6@krypton:/tmp/tmp.J1EBWzVpoy$ cat ciph
EICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZKTHNSIRFX
```

We can easily notice the string which is repeating: EICTDGYIYZKTHNSIRFXYCPFUEOCKRN EICTDGYIYZKTHNSIRFXYCPFUEOCKRN EICTDGYIYZKTHNSIRFXYCPFUEOCKRN ...
This is our cipher for plaintext of 'A's. If it were 'B's instead of 'A's, the output string letters would be shifted up by 1 character (E -> F, etc.).
Now we know that first character's ascii value is shifted up by 4 characters (A -> E), second one's raised by 8 (A -> I) and so on. We can create
an array consisting every shift value and decrease ascii values of cipher letters one by one. I'm gonna do it with Python:
```python
a = 'AAAAAAAAAAAAAAAAAAAAAAAAAAAAAA'
b = 'EICTDGYIYZKTHNSIRFXYCPFUEOCKRN'
c = 'PNUKLYLWRQKGKBE'
key = []
for i in range(len(a)):
    key.append(ord(b[i]) - ord(a[i]))
t = ''
for i in range(len(c)):
    if (ord(c[i]) - key[i])<65:
        t += chr(ord(c[i]) + (26-key[i]))
    else:
        t += chr(ord(c[i]) - key[i])
print(t)
```
Output:
```
LFSRISNOTRANDOM
```

Password: **LFSRISNOTRANDOM**


