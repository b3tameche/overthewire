Change directory to */krypton/krypton2* and list its items.

```
krypton2@krypton:~$ cd /krypton/krypton2
krypton2@krypton:/krypton/krypton2$ ls -l
total 24
-rwsr-x--- 1 krypton3 krypton2 9032 May 19  2020 encrypt
-rw-r----- 1 krypton3 krypton3   27 May 19  2020 keyfile.dat
-rw-r----- 1 krypton2 krypton2   13 May 19  2020 krypton3
-rw-r----- 1 krypton2 krypton2 1815 May 19  2020 README
```
Then we will follow instructions:

```
krypton2@krypton:/$ mktemp -d
/tmp/tmp.CbkqXjqhJe
krypton2@krypton:/$ cd /tmp/tmp.CbkqXjqhJe
krypton2@krypton:/tmp/tmp.CbkqXjqhJe$ ln -s /krypton/krypton2/keyfile.dat
krypton2@krypton:/tmp/tmp.CbkqXjqhJe$ chmod 777 .
```

We have created temporary directory as our workspace and made a symbolic link to **keyfile.dat**.
Then we gave user **krypton3** access to our working directory.

Since we know that next password is encrypted by ROT cipher, we can create a file **trick** containing single letter 'A'.
After that, we will encrypt it with given *encrypt* binary and expose the key.

```
krypton2@krypton:/tmp/tmp.CbkqXjqhJe$ vim trick
krypton2@krypton:/tmp/tmp.CbkqXjqhJe$ cat trick
A
krypton2@krypton:/tmp/tmp.CbkqXjqhJe$ /krypton/krypton2/encrypt trick
krypton2@krypton:/tmp/tmp.CbkqXjqhJe$ ls
ciphertext  keyfile.dat  trick
krypton2@krypton:/tmp/tmp.CbkqXjqhJe$ cat ciphertext
Mkrypton2@krypton:/tmp/tmp.CbkqXjqhJe$
```

We see that **encrypt** converted 'A' into 'M', so the key is 12. If we want to obtain password from */krypton/krypton2/krypton3*,
we have to use ROT14 algorithm on cipher to reverse the encryption.

```
krypton2@krypton:/$ cat /krypton/krypton2/krypton3
OMQEMDUEQMEK
```

Password: **CAESARISEASY**
