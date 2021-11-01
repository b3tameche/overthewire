Change directory to */krypton/krypton5* and list its files.
```
krypton5@krypton:~$ cd /krypton/krypton5
krypton5@krypton:/krypton/krypton5$ ls
found1  found2  found3  krypton6  README
```

Opening *found* files gave us strings:
```
krypton5@krypton:/krypton/krypton5$ cat found1
SXULW GNXIO WRZJG OFLCM RHEFZ ALGSP DXBLM PWIQT XJGLA RIYRI BLPPC HMXMG CTZDL CLKRU YMYSJ ...

krypton5@krypton:/krypton/krypton5$ cat found2
GLCYX UKFHS PEZXF AVJOW QQYYR RAYHM GIEOG ARIAZ YEYXV PXFPJ BXXUY SLELR NXHNH PLARX TADLC ...

krypton5@krypton:/krypton/krypton5$ cat found3
FIPJS EJXYV CYYHZ KMOYH GNEYN XSYSI PHJOM OKLYY HBTXH MLIYI RGGKK PMFHJ GMJRX GNOVT ZHCSL ...
```

As in Level 5, I'm not going to crack it manually. At first, I'll reveal the key using this [tool](https://www.dcode.fr/vigenere-cipher).

The key is: **KEYLENGTH**

Our ciphertext is: 
```
krypton5@krypton:/krypton/krypton5$ cat krypton6
BELOS Z
```

Now we just crack the ciphertext using the key obtained above and get: **RANDO M**

Password: **RANDOM**
