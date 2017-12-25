# DRDO CTF 2017 : Crypto-6

**Category:** Crypto

**Level:** Moderate

**Points:** 100

**Solves:** 37

**Description:**

Unit B captured a system having many classified information. A flag works as a key to that system. 
Any wrong key can destroy the system without extracting information. Unit A captured the flag and sent to Unit B so that unit B breaks the system immediately. As there was a chance that key can be tampered in between therefore unit A used a hash-like function (for integrity check) which outputs **5 bytes** for any input. 
Unit A provides the flag as an input to the function (unit B also has this function) and gets a 5 byte output. Unit A sends this 5 byte output to unit B so that unit B can verify that flag received by it was the correct one. In case the 5 bytes mismatch occurs unit B will not use the key and will request to resend the key.

But in reality unit A captured the correct flag and sent it to unit B with 5-bytes hash-like output. Unit B received the flag and calculated the 5-byte hash and matched it with the received hash. It matched and unit B inputs the key to the system and surprisingly system destroys. 
Diagram in the attachment depicts what happened: (Attacker changed **two characters of the flag(X,X) (case not changed)** such that **hash is still valid**) . Go ahead and find the complete flag.

![Scenario.png](Scenario.png)

Details of Hash functions are as follows:
Hash Function:
```
1st Byte: Addition/substraction/multiplication of following bytes of input string: 1,6,8,10,12… mod 256
2nd Byte: Addition/substraction/multiplication of following bytes of input string: 2,7,9,11,13… mod 256
3rd Byte: Addition/substraction/multiplication of following bytes of input string: 3,8,10,12,14… mod 256
4th Byte: Addition/substraction/multiplication of following bytes of input string: 4,9,11,13,15… mod 256
5th Byte: Addition/substraction/multiplication of following bytes of input string: 5,10,12,14,16… mod 256
```
Sample Hash Output:
```
String: The Agni ballistic missiles are a range of MRBMs, IRBMs, ICBMs meant for long-range deterrence. Hash: 3EBAD3520
String: The Trishul is a short range surface-to-air missile developed by India. Hash: BF2C5E7BDA
String: The Nag Anti-tank missile is a guided missile system intended for the Indian Air Force and the Indian Army. Hash: B45664A72D
String: The Shaurya missile is a canister-launched hypersonic surface-to-surface tactical missile developed by DRDO. Hash: 54C7FD1E76
String: The K-15 Sagarika is a nuclear-capable submarine-launched ballistic missile with a range of 750 kilometres. Hash: FE1CE2A393
```


## Write-up

1. The challenge descibe a hash function which doesn't fullfil requirement and produces same hash for different input. 

2. In the challenge statement partial flag is given, which is `DRDO@60_{A3X5X5}_FLAG!`, and missing two positions which are `X` needs to be find to get the complete flag.

3. It is clear in the challenge statement that `X` positions have been changed and case not changed(it means only UPPERCASE are valid becase `X` is in uppercase). That means those two `X` must be replaced by any uppercase character from `A` to `Z`.

4. Now you have to find out what is hash function. As mentioned in the statement that hash function is a combination of addition/substraction/multiplication and there is specfic way to find everybyte of hash. (Some of participants got confuesd that operations used in hashfunction are different for each byte but then it was cleared that hash function operations are same of each byte)

We can rewrite the hash function(H(x<sub>1</sub>,x<sub>2</sub>,x<sub>3</sub>,...)) as follows:

1 <sup>st</sup> Byte of Hash : 


## Python Program

```Python
#Hash Function

```
