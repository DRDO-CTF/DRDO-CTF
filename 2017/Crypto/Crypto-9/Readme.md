# DRDO CTF 2017 : Crypto-9

**Category:** Crypto

**Level:** Hard

**Points:** 200

**Solves:** 1

**Description:**

Early CCS or CCS Injection is a vulnerability which was discovered in OpenSSL in 2014. This vulnerability allows the server to accept the ChangeCipherSpec message (This message is used to inform that all message following this message are going to be encrypted) of TLS protocol earlier(before ClientKeyExchange message) than expected. 
Due to its early acceptance of CCS message **keys are not exchanged but encryption starts** and client sends an encrypted ClientKeyExchange message. This encrypted ClientKeyExchange message is similar to plain ClientKeyExchange message but it is encrypted due to early acceptance of CCS message. 
ClientKeyExchnage message contains an **encrypted PreMasterSecret which is encrypted using RSA-2048 public key**. Decrypt the contents to attached file of capture the FLAG.

**Hint:** You have to get the PreMasterSecret to capture the FLAG. 

## Additional Information

* TLS Version: 1.0
* Server Private key: cyber\_challenge.key
* PCAP: DecryptMe.pcapng
* Key\_Block.JPG, Master\_Secret.JPG, PRF\_Phash.JPG and rfc2246.txt will help you to understand the protocol and decrypt the content.


## Help
* In wireshark to see the captured packets as TLS message for port 1024:

Go to Wireshark->Analyze tab --> Decode As --> type port 1024 and select SSL protocol. Now it will show packets as SSL/TLS Messages from the port 1024

## Online Resources

* Internet Search: “CCS Injection”, CVE-2014-0224
* TLS 1.0 RFC: https://www.ietf.org/rfc/rfc2246.txt

## Attachments

[DecryptMe.pcapng](DecryptMe.pcapng)

[cyber_challenge.key](cyber_challenge.key)

[rfc2246.txt](rfc2246.txt)

![Key\_Block.JPG](Key\_Block.JPG)

![Master\_Secret.JPG](Master\_Secret.JPG)

![PRF\_PHash.JPG](PRF\_PHash.JPG)


## Write-up

1. This challenges was more focused on implementing the given process rather than finding the process. It was clearly mentioned that the traffic given was affected by early CCS and due to which ClientKeyExchange handshake message got encrypted . Therefore, the task was to decrypt the ClientKeyExchange message and get the RSA encrypted PreMasterSecret and then decrypt it using given RSA private Key.

2. For those who doesn't know about TLS: (You can refer to http://blog.catchpoint.com/2017/05/12/dissecting-tls-using-wireshark/ for a summary)

* TLS is `Transport Layer Secryity` which is used world wide to provide secure communication between the devices. Internet is one of the major infrastructure which uses the TLS. All `https` connections use TLS protocol. SSL `Secure Socket Layer` was predecessor of TLS. TLS started with version 1.0 and then upgraded to 1.1 and then to 1.2. TLS 1.3 is still in draft but has been already implemented by most of the libraries. 

* TLS communication can be divided in two parts. First part is handsahke where both the parties agree on common available parameters like KeyExchangeMechanim, DataEncryptionAlgorithm, HashFunction etc. Once both parties agrees and exchange required paramters, encrypted commuincation starts.

Following Diagram depicts the hanshake process:

![TLS\_Handshake.png](TLS\_Handshake.png)


* You can see in the daigram that except `Finish` message, all messages of handshake are in plain. Data encrption starts when
`Finish` message exchange is complete. 

* `ClientKeyExchange` contains a valuale information, called `PreMasterSecret`, which is a secret parameter sent from client to the server. To ensure the secrecy `PreMasterSecret` is encrypted with RSA public key and sent to the server. 

Following diagram shows a general structure of `ClientKeyExchange` message for RSA based KeyExchange. 

![ClientKeyExchange.png](ClientKeyExchange.png)

You can see that `PreMasterSecret` is encrypted with RSA public key.
## Python Program
