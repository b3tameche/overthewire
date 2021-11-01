As always,
```
krypton4@krypton:~$ cd /krypton/krypton4
krypton4@krypton:/krypton/krypton4$ ls
found1  found2  HINT  krypton5  README

krypton4@krypton:/krypton/krypton4$ cat found1
YYICS JIZIB AGYYX RIEWV IXAFN JOOVQ QVHDL CRKLB SSLYX RIQYI IOXQT WXRIC RVVKP BHZXI ...

krypton4@krypton:/krypton/krypton4$ cat found2
YYIIA CWVSL PGLVH DSAFD TYYRY YEDRG LYXER BJIEV EPLVX BICNE XRIDT IICXD TIXRI PJNIB ...

krypton4@krypton:/krypton/krypton4$ cat HINT
Frequency analysis will still work, but you need to analyse it
by "keylength".  Analysis of cipher text at position 1, 6, 12, etc
should reveal the 1st letter of the key, in this case.  Treat this as
6 different mono-alphabetic ciphers...

Persistence and some good guesses are the key!
```

Manual decryption would take quite some time, so I diceded to reveal key using online [tool](https://www.dcode.fr/vigenere-cipher).

It easily cracked the key: **FREKEY**
Our ciphertext:
```
krypton4@krypton:/krypton/krypton4$ cat krypton5
HCIKV RJOX
```

Now we can use same tool for decryption since we know the key. It returned **CLEAR TEXT**.

Password: **CLEARTEXT**
