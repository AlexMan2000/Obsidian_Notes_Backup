# Preliminaries
## Detailed Definition of Confidentiality
> [!def]
> ![](2_Symmetric_Cryptography.assets/image-20240227215634812.png)![](2_Symmetric_Cryptography.assets/image-20240227215646693.png)
> A more formal, rigorous definition of confidentiality is: **the ciphertext C should give the attacker no additional information about the message M**. 
> 
> In other words, the attacker should not learn any new information about M beyond what they already knew before seeing C (seeing C should not give the attacker any new information).


## IND-CPA Definition of Confidentiality
### IND-CPA Definition
> [!def]
> This definition is called IND-CPA (indistinguishability under chosen plaintext attack.
> ![](2_Symmetric_Cryptography.assets/image-20240227220904359.png)![](2_Symmetric_Cryptography.assets/image-20240227220910596.png)
> 
> There are a few important caveats to the IND-CPA game to make it a useful, practical security definition:
> 



### Edge Case 1: Len(M0) == Len(M1)
> [!def]
> _The messages M0 and M1 must be the same length._ 
> ![](2_Symmetric_Cryptography.assets/image-20240227222545139.png)
> **Remarks:**
> 1. If we want to hide message length from the attacker, then we must incorporate message length as a component of our encryption scheme. For example, shorter plaintext may result in shorter ciphertext as a result, which gives the attacker some clue about your encryption scheme. So the more you try to hide from the attack, the more dimension you are giving your attackers to infiltrate your encryption system. In practice, if you want to hide message length, then all the plaintext should have the same length for simplicity and efficiency considerations. But this is not practical, as shown in the graph above.
> 2. If we didn’t force M0 and M1 to be the same length, then our game would incorrectly mark some IND-CPA secure schemes as insecure. In particular, if a scheme leaks the plaintext length, it can still be considered IND-CPA secure. However, Eve would win the IND-CPA game with this scheme, since she can send a short message and a long message, see if Alice sends back a short or long ciphertext, and distinguish which message was sent. To account for the fact that cryptosystems can leak plaintext length, we use equal-length messages in the IND-CPA game. **In other words**, we want IND-CPA definition of confidentiality to match with the real-world cryptographic system where plaintext length is allowed to leak(i.e. length doesn't give attacker any information, so better leak to them since they are useless anyway). So by enforcing M0 and M1 to be of the same length, we consider into the fact that plaintext length doesn't give attacker new information.
> 3. Simply input, in reality, leaking plaintext length is secure. If we don't enforce len(M0) == len(M1), then in order for IND-CPA definition to work, even if we leak len(M0) and len(M1), attacker cannot have more information. But by the game scheme, message length could give attacker more information, classifying the supposed secure encryption as insecure. 
> 
> 


### Edge Case 2: Attacker Runtime
> [!def]
> _Eve is limited to a practical number of encryption requests._ In practice, some schemes may be vulnerable to attacks but considered secure anyway, because those attacks are computationally infeasible. For example, Eve could try to brute-force a 128-bit secret key, but this would take 21282128 computations. If each computation took 1 millisecond, this would take 10281028 years, far longer than the age of our solar system. These attacks may be theoretically possible, but they are so inefficient that we don’t need to worry about attackers who try them.
> ![](2_Symmetric_Cryptography.assets/image-20240227222947475.png)
> To account for these computationally infeasible attacks in the IND-CPA game, we limit Eve to a practical number of encryption requests. One commonly-used measure of practicality is polynomially-bounded runtime: any algorithm Eve uses during the game must run in $O(n^k)$ time, for some constant $k$.


### Edge Case 3:  Negligible Advantage
> [!def]
> _Eve only wins if she has a non-negligible advantage._ Consider a scheme where Eve can correctly tell which message was sent with probability $1/2+1/2^{128}$. This number is greater than $1/2^{128}$, but Eve’s advantage is $1/2^{128}$, which is astronomically small. In this case, we say that Eve has _negligible_ advantage–the advantage is so small that Eve cannot use it to mount any practical attacks. For example, the scheme might use a 128-bit key, and Eve can break the scheme if she guesses the key (with probability $1/2^{128}$). 
> 
> Although this is theoretically a valid attack, the odds of guessing a 128-bit key are so astronomically small that we don’t need to worry about it. The exact definition of negligible is beyond the scope of this class, but in short, Eve only wins the IND-CPA game if she can guess which message was sent with probability greater than 1/2+n, where n is some non-negligible probability.
> ![](2_Symmetric_Cryptography.assets/image-20240227224848609.png)


## XOR Review
> [!def]
> ![](2_Symmetric_Cryptography.assets/image-20240302223519182.png)![](2_Symmetric_Cryptography.assets/image-20240302223527127.png)



# Symmetric-Key Encryption
> [!def]
> ![](2_Symmetric_Cryptography.assets/image-20240227215254603.png)![](2_Symmetric_Cryptography.assets/image-20240227215312831.png)![](2_Symmetric_Cryptography.assets/image-20240227215329622.png)




# One-Time Pad Scheme
## Algorithm
> [!overview]
> ![](2_Symmetric_Cryptography.assets/image-20240302224557688.png)

> [!algo]
> ![](2_Symmetric_Cryptography.assets/image-20240302224745543.png)![](2_Symmetric_Cryptography.assets/image-20240302224654308.png)![](2_Symmetric_Cryptography.assets/image-20240302224702161.png)




## Correctness
> [!important]
> ![](2_Symmetric_Cryptography.assets/image-20240302224840237.png)



## Security
> [!important]
> ![](2_Symmetric_Cryptography.assets/image-20240302224910773.png)![](2_Symmetric_Cryptography.assets/image-20240302225003575.png)





## Issues - Reuse of Key
> [!bug] Caveats
> ![](2_Symmetric_Cryptography.assets/image-20240302225311740.png)![](2_Symmetric_Cryptography.assets/image-20240302225320254.png)![](2_Symmetric_Cryptography.assets/image-20240302225329604.png)![](2_Symmetric_Cryptography.assets/image-20240302230906119.png)
> The reason why we choose $M_0=0^k$ is that $M_{0}\oplus K=K$ and $K$ is reused across multiple queries. So if you send $M_0$ again you will get the same encryption due to the deterministic essence of the algorithm.
> 
> Because IND-CPA requires the reuse of key, OTP is insecure under this definition.
> 
> ![](2_Symmetric_Cryptography.assets/image-20240302230947692.png)



## Impractibility
> [!important]
> ![](2_Symmetric_Cryptography.assets/image-20240302225503514.png)



# Block Cipher Scheme
## Motivation
> [!motiv] Motivation
> As we’ve just seen, generating new keys for every encryption is difficult and expensive. Instead, in most symmetric encryption schemes, Alice and Bob share a secret key and use this single key to repeatedly encrypt and decrypt messages. The **block cipher** is a fundamental building block in implementing such a **symmetric encryption** scheme.


## Block Cipher
> [!def]
> Intuitively, a block cipher transforms a fixed-length, n-bit input into a fixed-length n-bit output. The block cipher has $2^k$ different settings for scrambling, so it also takes in a k-bit key as input to determine which scrambling setting should be used. Each key corresponds to a different scrambling setting. The idea is that an attacker who doesn’t know the secret key won’t know what mode of scrambling is being used, and thus won’t be able to decrypt messages encrypted with the block cipher.
> 
> A block cipher has two operations: encryption takes in an n-bit plaintext and a k-bit key as input and outputs an n-bit ciphertext. Decryption takes in an n-bit ciphertext and a k-bit key as input and outputs an n-bit plaintext. 
> 
> **Question: why does the decryption require the key as input?**
> 
> The key is needed to determine which scrambling setting was used to generate the ciphertext. If decryption didn’t require a key, any attacker would be able to decrypt encrypted messages!
> ![](2_Symmetric_Cryptography.assets/image-20240303121419899.png)
> 
> Given a fixed scrambling setting (key), the block cipher encryption must map each of the $2^n$ possible plaintext inputs to a different ciphertext output. In other words, given a specific key, the block cipher encryption must be able to map every possible input to a unique output. 
> 
> If the block cipher mapped two plaintext inputs to the same ciphertext output, there would be no way to decrypt that ciphertext back into plaintext, since that ciphertext could correspond to multiple different plaintexts. This means that the block cipher must also be _deterministic_. Given the same input and key, the block cipher should always give the same output.
> 
> In mathematical notation, the block cipher can be described as follows. There is an encryption function $E:\{0,1\}^k×\{0,1\}^n→\{0,1\}^n$.
> 
> This notation means we are mapping a k-bit input (the key) and an n-bit input (the plaintext message) to an n-bit output (the ciphertext). Once we fix the key K, we get a function mapping n bits to n bits: $E_{K}:\{0,1\}^n→\{0,1\}^n$ defined by $E_K(M)=E(K,M)$. $E_K$ is required to be a _permutation_ on the n-bit strings, in other words, it must be an invertible (bijective) function. 
> 
> The inverse mapping of this permutation is the decryption algorithm $D_K$. In other words, decryption is the reverse of encryption: $D_K(E_K(M))=M$.
> 
> The block cipher as defined above is a category of functions, meaning that there are many different implementations of a block cipher. Today, the most commonly used block cipher implementation is called **Advanced Encryption Standard** (AES). It was designed in 1998 by Joan Daemen and Vincent Rijmen, two researchers from Belgium, in response to a competition organized by NIST.



## Correctness
> [!def]
> ![](2_Symmetric_Cryptography.assets/image-20240303121925474.png)
> Proof by contrapositive and contradiction technique used here.



## Security
> [!bug] IND-CPA Insecurity
> Block ciphers, including AES, are not IND-CPA secure on their own because they are deterministic. In other words, encrypting the same message twice with the same key produces the same output twice. The strategy that an adversary, Eve, uses to break the security of AES is exactly the same as the strategy from the one-time pad with key reuse. Eve sends $M_0$ and $M_1$ to the challenger and receives either $E(K,M_0)$ or $E(K,M_1)$. She then queries the challenger for the encryption of $M_0$ and receives $E(K,M_0)$. 
> 
> If the two encryptions she receives from the challenger are the same, then Eve knows the challenger encrypted $M_0$ and sent $E(K,M_0)$. 
> 
> If the two encryptions are different, then Eve knows the challenger encrypted $M_1$ and sent $E(K,M_1)$. Thus Eve can win the IND-CPA game with probability 100% >1/2, and the block cipher is not IND-CPA secure.
> 

> [!important] Computationally Indistinguishable from Random Permutation
> Although block ciphers are not IND-CPA secure, they have a desirable security property that will help us build IND-CPA secure symmetric encryption schemes: namely, a block cipher is _computationally indistinguishable_ from a random permutation. In other words, for a fixed key K�, EK�� “behaves like” a random permutation on the n�-bit strings.
> 
> A random permutation is a function that maps each n�-bit input to exactly one random n�-bit output. One way to generate a random permutation is to write out all 2n2� possible inputs in one column and all 2n2� possible outputs in another column, and then draw 2n2� random lines connecting each input to each output. Once generated, the function itself is not random: given the same input twice, the function gives the same output twice. However, the choice of which output is given is randomly determined when the function is created.
> ![](2_Symmetric_Cryptography.assets/image-20240303121933937.png)






