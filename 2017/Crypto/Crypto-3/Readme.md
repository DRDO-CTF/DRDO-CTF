# DRDO CTF 2017 : Crypto-3

**Category:** Crypto

**Level:** Easy

**Points:** 50

**Solves:** 12

**Description:**

A message is intercepted with 3 keys. Without knowing the algorithm it became impossible to break the message but the smarter one read the problem again and again and broke the message using 3 keys sequentially. Let’s see how smart you are.

`Keys: AKASH, AGNI_{KALAM} ,PRITHVI`

`CryptMessage: 7EBD50AC41E781BDB815D6A30537A17B013137F783BE627C`

## Write-up

1. There are 3 keys and these are used sequentially. This hint clealy indicates the algorithm used was `3-DES`. 

2. Order of key in the challenges is not same as it was used for encryption/decryption. Therefore you need to try all possible combination. There are 6 possilbe combination (3x2x1) and you need to try each combination to get the plaintext. You can try these combinations at http://tripledes.online-domain-tools.com/ with CBC mode and all `00` IV. (CBC mode is one of the standard mode and if not specified IV is all `00`)

3. After all try it is found that correct sequence of keys is `PRITHVI,AKASH,AGNI_{KALAM}`. You can use this key to decrypt the CryptMessage (at http://tripledes.online-domain-tools.com/) and get the flag.

4. Flag is `DRDO@60_{OQ406H}_FLAG!`


## Python Program

```Python
from Crypto.Cipher import DES3
key = 'PRITHVIAKASHAGNI_{KALAM}'
crypt = '7EBD50AC41E781BDB815D6A30537A17B013137F783BE627C'
cipher = DES3.new(bytes(bytearray.fromhex(key.encode('hex'))), DES3.MODE_CBC, 8 * '\x00')
cipher.decrypt(bytes(bytearray.fromhex(crypt)))
#output is 'DRDO@60_{OQ406H}_FLAG!\x00\x00'
```
