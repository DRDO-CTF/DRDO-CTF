# DRDO CTF 2017 : Crypto-1

**Category:** Crypto

**Level:** Easy

**Points:** 50

**Solves:** 75

**Description:**

>A Commander got a **HEXADECIMAL** message and an image but doesn’t know how to read it. He called a cryptographer and asked for help. The cryptographer solved it and said its **perfect secrecy**. Lets see if you can solve it. <br/>
>`Crypt-Message: 0A130607127764113A6A227416106F340B0E0D08155C`

![NABHRATNA.jpg](NABHRATNA.jpg)

## Write-up

>1. Perfect Secrecy means it is One-Time-Pad which is bascially byteswise XOR of key and plaintext.<br/>
>(You can use http://xor.pw/# for XOR operation)<br/>
>2. Open the image in hex-editor. Last bytes in the image are key bytes.<br/>
>![hex\_key.png](hex_key.png)<br/>
>Therefore key is: ``NABHRATNA_{FLYWITHAIR}`` which is of exactly same length as the crypt-message.<br/>
>3. Now byteswise XOR of crypt message and key will result in the flag.<br/>
>4. Flag is : `DRDO@60_{5Y2ZI8}_FLAG!`
## Python Program

```Python
key = "NABHRATNA_{FLYWITHAIR}"
crypt = "0A130607127764113A6A227416106F340B0E0D08155C".decode('hex')
plain_hex = ''.join(hex(ord(a) ^ ord(b))[2:].zfill(2) for a,b in zip(key,crypt))
plain_hex.decode('hex')
#Output is 'DRDO@60_{5Y2ZI8}_FLAG!'
```
