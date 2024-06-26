# Writeup OverTheWire: Krypton
The Krypton wargame.

## Level 0
### Level Info
Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:

S1JZUFRPTklTR1JFQVQ=
Use this password to log in to krypton.labs.overthewire.org with username krypton1 using SSH on port 2231. You can find the files for other levels in /krypton/

### Solution

1. Find a Base64 decryptor such as [CyberChef](https://gchq.github.io/CyberChef/).
2. Input the Base64 string, make sure that the CyberChef 'operation' menu is set to **from Base64**. https://en.wikipedia.org/wiki/Base64
3. Copy the output text to your clipboard.
4. SSH into Krypton's server.
```sh
ssh krypton1@krypton.labs.overthewire.org -p 2231
```
5. Input the password when prompted.
```sh
krypton1@krypton.labs.overthewire.org's password:[PASTE FROM CLIPBOARD HERE]
```
6. You have successfully entered the Krypton server. Go to /krypton and see the files inside.
```sh
$ cd /krypton
$ ls -la
```
7. Go to /krypton/krypton1 and see the files inside
```sh
$ cd krypton1
$ ls -la
```
8. Proceed to the next level.

### Flag
`KRYPTONISGREAT`

## Level 1
### Level Info
The password for level 2 is in the file ‘krypton2’. It is ‘encrypted’ using a simple rotation. It is also in non-standard ciphertext format. When using alpha characters for cipher text it is normal to group the letters into 5 letter clusters, regardless of word boundaries. This helps obfuscate any patterns. This file has kept the plain text word boundaries and carried them to the cipher text. Enjoy!

### Solution

1. Read the file encrypted file 'krypton2'
```sh
cat krypton2
```
2. The most simple rotation encryption is ROT13. Which is a caesar cipher that rotates alphabet by a specific amount (default is 13.) https://en.wikipedia.org/wiki/ROT13
3. Input the ROT13 string, make sure that the CyberChef 'operation' menu is set to **ROT13** if you're sure about the amount of rotation or alternatively use **ROT13 BRUTEFORCE**. 
3. Copy the output text to your clipboard.
4. SSH into Krypton's server.
```sh
ssh krypton2@krypton.labs.overthewire.org -p 2231
```
5. Input the password when prompted.
```sh
krypton1@krypton.labs.overthewire.org's password:[PASTE FROM CLIPBOARD HERE]
```
6. Continue to the next level.

### Flag
`LEVEL TWO PASSWORD ROTTEN`

## Level 2
### Level Info
ROT13 is a simple substitution cipher.

Substitution ciphers are a simple replacement algorithm. In this example of a substitution cipher, we will explore a ‘monoalphebetic’ cipher. Monoalphebetic means, literally, “one alphabet” and you will see why.

This level contains an old form of cipher called a ‘Caesar Cipher’. A Caesar cipher shifts the alphabet by a set number. For example:

plain:  a b c d e f g h i j k ...
cipher: G H I J K L M N O P Q ...
In this example, the letter ‘a’ in plaintext is replaced by a ‘G’ in the ciphertext so, for example, the plaintext ‘bad’ becomes ‘HGJ’ in ciphertext.

The password for level 3 is in the file krypton3. It is in 5 letter group ciphertext. It is encrypted with a Caesar Cipher. Without any further information, this cipher text may be difficult to break. You do not have direct access to the key, however you do have access to a program that will encrypt anything you wish to give it using the key. If you think logically, this is completely easy.

One shot can solve it!

Have fun.

Additional Information:

The encrypt binary will look for the keyfile in your current working directory. Therefore, it might be best to create a working direcory in /tmp and in there a link to the keyfile. As the encrypt binary runs setuid krypton3, you also need to give krypton3 access to your working directory.

Here is an example:

```sh
krypton2@melinda:~$ mktemp -d
/tmp/tmp.Wf2OnCpCDQ
krypton2@melinda:~$ cd /tmp/tmp.Wf2OnCpCDQ
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ln -s /krypton/krypton2/keyfile.dat
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ls
keyfile.dat
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ chmod 777 .
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ /krypton/krypton2/encrypt /etc/issue
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ls
ciphertext  keyfile.dat
```

### Solution

1. Read the file encrypted file 'krypton2'
```sh
ls /krypton/krypton2
```
2. Make a temporary workstation directory and test the encrypt binary as instructed:
```
mktemp -d
cd /tmp/tmp.Hf5tZxjkmp
ln -s /krypton/krypton2/keyfile.dat
ls
chmod 777 .

/krypton/krypton2/encrypt /etc/issue
ls
```
3. make a textfile `test.txt` and input abcd to test the encryption binary (/krypton/krypton2/encrypt)
```sh
echo "abcd" > test.txt
```
4. Use the encryption binary on test.txt and see the result
```
/krypton/krypton2/encrypt test.txt
ls
cat ciphertext
```
5. Using CyberChef's, **ROT13 Brute Force**, input `abcde` and find rotate amount where the result is the same as the `ciphertext` above.
6. I found the ciphertext where the amount is `12` which means that the rotation must be done by 12 places -- we can decrypt the cipher by moving the ciphertext by -12 places. 
7. Finally, using the RO13 set the amount to -12 and enter `ciphertext` to confirm and input /krypton/krypton2/krypton3 to get the flag
8. Copy the output text to your clipboard.
9. SSH into Krypton's server.
```sh
ssh krypton2@krypton.labs.overthewire.org -p 2231
```
10. Input the password when prompted.
```sh
krypton1@krypton.labs.overthewire.org's password:[PASTE FROM CLIPBOARD HERE]
```
11. Continue to the next level.

### Flag
`CAESARISEASY`

## Level 3
### Level Info
The password for level 2 is in the file ‘krypton2’. It is ‘encrypted’ using a simple rotation. It is also in non-standard ciphertext format. When using alpha characters for cipher text it is normal to group the letters into 5 letter clusters, regardless of word boundaries. This helps obfuscate any patterns. This file has kept the plain text word boundaries and carried them to the cipher text. Enjoy!

### Solution

1. Read the file encrypted file 'krypton2'
```sh
cat krypton2
```
2. The most simple rotation encryption is ROT13. Which is a caesar cipher that rotates alphabet by a specific amount (default is 13.) https://en.wikipedia.org/wiki/ROT13
3. Input the ROT13 string, make sure that the CyberChef 'operation' menu is set to **ROT13** if you're sure about the amount of rotation or alternatively use **ROT13 BRUTEFORCE**. 
3. Copy the output text to your clipboard.
4. SSH into Krypton's server.
```sh
ssh krypton2@krypton.labs.overthewire.org -p 2231
```
5. Input the password when prompted.
```sh
krypton1@krypton.labs.overthewire.org's password:[PASTE FROM CLIPBOARD HERE]
```
6. Continue to the next level.

### Flag
`LEVEL TWO PASSWORD ROTTEN`


