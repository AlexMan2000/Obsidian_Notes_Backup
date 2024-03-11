# MAC
## Definition
> [!def]
> ![](4_Message_Authentication_Codes.assets/image-20240309112923039.png)
> Formally, the MAC on a message M is a value F(K,M) computed from K and M; the value F(K,M) is called the _tag_ for M or the MAC of M. Typically, we might use a 128-bit key K and 128-bit tags.
> [!example] MAC on File Storage

> [!example] MAC on File Storage
> MACs can be used for more than just communication security. For instance, suppose we want to store files on a removable USB flash drive, which we occasionally share with our friends. To protect against tampering with the files on our flash drive, our machine could generate a secret key and store a MAC of each file somewhere on the flash drive. When our machine reads the file, it could check that the MAC is valid before using the file contents. In a sense, this is a case where we are “communicating” to a “future version of ourselves,” so security for stored data can be viewed as a variant of communication security.


## MAC Usage
> [!important]
> ![](4_Message_Authentication_Codes.assets/image-20240309114444301.png)



## Security - EU-CPA
> [!def]
> Given a secure MAC algorithm F, if the attacker replaces M by some other message M, then the tag will almost certainly no longer be valid: in particular, F(K,M)≠F(K,M′) for any M≠M' .
> 
> Given M and T=F(K,M), an attacker who does not know the key K should be unable to find a different message M′ and a tag T′ such that T′ is a valid tag on M′ (i.e., such that T′=F(K,M′)). 
> 
> - Secure MACs are designed to ensure that **even small changes to the message make unpredictable changes to the tag**, so that the adversary cannot guess the correct tag for their malicious message M′.
> - Secure MACs are designed to be deterministic. Calling F(K,M) twice gives the same output.
> - For secure MACs, even if Eve observes a bunch of message-tag pair $\langle M_{1},T_{1}\rangle,\langle M_{2},T_{2}\rangle,\cdots, \langle M_{n},T_{n}\rangle$, we still **cannot** find a valid tag $T'$ for an unseen message $M'\notin\{M_{1},M_{2},\cdots,M_{n}\}$. 
> 
> ![](4_Message_Authentication_Codes.assets/image-20240309114055955.png)

> [!property]
> ![](4_Message_Authentication_Codes.assets/image-20240309113005906.png)![](4_Message_Authentication_Codes.assets/image-20240309113012987.png)



# Build Secure MACs
## AES-EMAC

 

## NMAC



## HMAC





# Authenticated Encrpytion