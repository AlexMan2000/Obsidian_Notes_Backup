# Digital Signatures
## Definition
> [!def]
> ![](2_Digital_Signatures.assets/image-20240523201653808.png)![](2_Digital_Signatures.assets/image-20240523201950284.png)



## Integrity: EU-CPA
> [!important]
> ![](2_Digital_Signatures.assets/image-20240523202815476.png)



## Digital Signatures in Practice
> [!important]
> ![](2_Digital_Signatures.assets/image-20240523202914163.png)






# RSA Signatures
## Intuition
> [!overview]
> We have a message M, and we want to sign it with a digital signature. 
> - This signature can only be computed by those who has the private key.
> - Anyone who has the private key can sign messages.
> 
> The formula to find the signature of message M is the following equation:
> $$H(M) = F_{U}(S)$$
> - Intuitively, finding $S$ requires us to know the inverse of function $F$.
> - By design, this inverse should be computationally hard to find without the private key $K$ that is generated alongside with the public key $U$.
> 
> Anyone with the $(U, K)$ pair can compute $S$ by $S=F^{-1}(H(M))$.



## Mathematical Background
> [!thm]
> ![](2_Digital_Signatures.assets/image-20240523230326078.png)



## Algorithm
> [!algo]
> ![](2_Digital_Signatures.assets/image-20240523230337235.png)![](2_Digital_Signatures.assets/image-20240523202935618.png)




## Security 
> [!def]
> ![](2_Digital_Signatures.assets/image-20240523231232039.png)





