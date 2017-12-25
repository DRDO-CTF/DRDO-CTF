# DRDO CTF 2017 : Crypto-5

**Category:** Crypto

**Level:** Easy

**Points:** 50

**Solves:** 2

**Description:**

Captain got a **CHARACTER** Message with **SPECIAL** private key. Let him know the message.

`7FE22E7E9BE293481407F1BEB470BB1D82A576D3EE6A55C4F1304614F642B14286BD051EA13CB92AB55DA7ACACDC558A45FC409F69866BC46738DB3D622F32A5390F33778C1E0643D7622888AE76BA829A1EA359CAFC2FFBD6182A9F3DDFB7CE1B71858A39FE2E64F693D4D55ED740FD36E018EE4B8EA505C2E1971AFAB0716EBBAC65DF1901F5864BA7C18243F0C28D4BEFDB4A0E4305B7FCF096D39C2FD348BFE3E2E8455BA0BFF267439199DBCE0A55DAEDC1E752D3A591CF82A15985AC452690119412EF3F2FFF4D0D9BFB145BCFDC0B17724C544197D9D0A0FED1D53F486DAD982C1814AAAA6CE5E72D0D70F358B204069570F2FE0061B88471845EF8B8`


Hint: **Password Length < 15**

[private.key](private.key)

## Write-up

1. You need to decrypt the RSA encrypted message using given RSA private Key. The private key is password protected and you need to get the password to use that private key.

2. Direct hint in the challenge is that password lenght is less than 15. Indirect hint, given in the challenge statement, is  `SPECIAL CHARACTER`. This means password consists of only special characters. 

3. Now you need to brute force the password. 

4. After sequentialy bruteforce you will find that password is of only 5 characters.(Designer wanted participants to write the program for bruteforce. If someone has implemented it then breaking 5 special characters password is easy).

Password is : !^$@$

5. You can use this password to while decryping using RSA private key. Decrypted content is the flag

Flag is : `DRDO@60_{J5YF38}_FLAG!`

## Python Program

```Python

from Crypto.PublicKey import RSA
f = open('private.key','r')
data = f.read()
import itertools

class GotTheFlag( Exception ):
    pass
try: 
    stuff = ['!', '@', '#','$','%','^','&','*','(',')','-','~']
    for L in range(1, 15):
        print "Checking Length: " + str(L) + "\n"
        for subset in itertools.product(stuff, repeat=L):
            try:
                password_try =  (' '.join(subset)).replace(' ','')
                key = RSA.importKey(data,password_try)
                crypt ="7FE22E7E9BE293481407F1BEB470BB1D82A576D3EE6A55C4F1304614F642B14286BD051EA13CB92AB55DA7ACACDC558A45FC409F69866BC46738DB3D622F32A5390F33778C1E0643D7622888AE76BA829A1EA359CAFC2FFBD6182A9F3DDFB7CE1B71858A39FE2E64F693D4D55ED740FD36E018EE4B8EA505C2E1971AFAB0716EBBAC65DF1901F5864BA7C18243F0C28D4BEFDB4A0E4305B7FCF096D39C2FD348BFE3E2E8455BA0BFF267439199DBCE0A55DAEDC1E752D3A591CF82A15985AC452690119412EF3F2FFF4D0D9BFB145BCFDC0B17724C544197D9D0A0FED1D53F486DAD982C1814AAAA6CE5E72D0D70F358B204069570F2FE0061B88471845EF8B8" 
                plain_text=key.decrypt(bytes(bytearray.fromhex(crypt)))
                print plain_text[-23:]
                raise GotTheFlag
            except ValueError:
                continue
except GotTheFlag:
    pass
#output is 
#Checking Length: 1

#Checking Length: 2

#Checking Length: 3

#Checking Length: 4

#Checking Length: 5

#DRDO@60_{J5YF38}_FLAG!
```
