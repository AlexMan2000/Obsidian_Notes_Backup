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
> Remarks:
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
> _Eve only wins if she has a non-negligible advantage._ Consider a scheme where Eve can correctly which message was sent with probability $1/2+1/2^{128}$. This number is greater than $1/2^{128}$, but Eve’s advantage is $1/2^{128}$, which is astronomically small. In this case, we say that Eve has _negligible_ advantage–the advantage is so small that Eve cannot use it to mount any practical attacks. For example, the scheme might use a 128-bit key, and Eve can break the scheme if she guesses the key (with probability $1/2^{128}$). 
> 
> Although this is theoretically a valid attack, the odds of guessing a 128-bit key are so astronomically small that we don’t need to worry about it. The exact definition of negligible is beyond the scope of this class, but in short, Eve only wins the IND-CPA game if she can guess which message was sent with probability greater than 1/2+n, where n is some non-negligible probability.
> ![](2_Symmetric_Cryptography.assets/image-20240227224848609.png)











## XOR Review



# Symmetric-Key Encryption
> [!def]
> ![](2_Symmetric_Cryptography.assets/image-20240227215254603.png)![](2_Symmetric_Cryptography.assets/image-20240227215312831.png)![](2_Symmetric_Cryptography.assets/image-20240227215329622.png)




# One-Time Pad Scheme




# Block Cipher Scheme