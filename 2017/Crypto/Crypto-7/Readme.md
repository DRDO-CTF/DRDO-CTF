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

