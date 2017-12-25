# DRDO CTF 2017 : Crypto-7

**Category:** Crypto

**Level:** Hard

**Points:** 200

**Solves:** 22

**Description:**

Two army units want to communicate to each other and need a system to provide confidentiality, integrity and authentication. A **Diffie-Hellman key exchange** based system has been designed to meet the requirements. 
The mechanism is explained in the attached diagram using a sample communication.

![SampleCommunication.png](SampleCommunication.png)

AES-crypt in the given Image is:

`9232B495D5E647E4D6676ADBA85910796A6E0FBE41D765FE8FC301310ECF9605284DEF29EA6238283B2FD2DD2A104BD6C267A1FB72D259BB084AED33D29D2A8CE48E852BEC43A3F929524EB35D15D2F4`

Although system was secure but due to use of weak parameters it is possible to break the system. Analysis of system revealed following weaknesses:

1. `Generator g<25 and 400<q<700`
2. `100 < a , b < 1500 and a + b = 2298`

You have to break sample encryption and authentication system to capture the flag. Move ahead **Step by Step**.


## Write-up

1. As mentioned in challenge statement, Diffie-hellman key exchange mechanism is used here. Serect in DH is g<sup>(ab)</sup> which can only be known if `a` and `b` are known to both parites. `a` and `b` are never exchanged in DH and only g<sup>a</sup>, g<sup>b</sup> are exchanged. 

2. First step would be to find the secret value which is g<sup>(ab)</sup>. To find it following condition are given in challenge.

* `Generator g<25 and 400<q<700`
* `100 < a , b < 1500 and a + b = 2298`

Now we need to bruteforce for the value of a and b to find g<sup>(ab)</sup>. 

While writing the bruteforce it can be observed that both `a,b >= 799` because to achieve the addition `2298` if one parameter is maximum `1499` then other has to minimum `799`. 
Therfore second codition could be modified to `798 < a , b < 1500 and a + b = 2298`

## Python Program
