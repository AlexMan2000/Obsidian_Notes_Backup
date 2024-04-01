# 1D Convolution
## Definition
> [!def]
> Also See [Convolution](../../Signal_Processing/1_LTI_Systems/Signals_LTI_Systems.md#Convolution)
> ![](Convolution_Operation.assets/image-20240319120800576.png)



## Computation Methods
> [!def]
> ![](Convolution_Operation.assets/image-20240319121421208.png)![](Convolution_Operation.assets/image-20240319121429820.png)![](Convolution_Operation.assets/image-20240319121438327.png)



# 2D Convolution
## Definition
> [!def]
> ![](Convolution_Operation.assets/image-20240319121541506.png)![](Convolution_Operation.assets/image-20240319121634565.png)




## Computation Methods
> [!important]
> ![](Convolution_Operation.assets/image-20240319121615088.png)![](Convolution_Operation.assets/image-20240319121622914.png)



# Convolutional Layer
> [!motiv]
> ![](Convolution_Operation.assets/image-20240328175206339.png)![](Convolution_Operation.assets/image-20240328175253196.png)




## Definition
> [!def]
> ![](Convolution_Operation.assets/image-20240328175330403.png)![](Convolution_Operation.assets/image-20240328175337092.png)![](Convolution_Operation.assets/image-20240328175419722.png)![](Convolution_Operation.assets/image-20240328175429195.png)



## Weight Sharing
> [!def]
> ![](Convolution_Operation.assets/image-20240328182900107.png)




## Padding
> [!def]
> ![](Convolution_Operation.assets/image-20240328182935933.png)
> **In summary, we have three paddings:**
> 1. Zero padding
> 2. Mirror Padding
> 3. **Same Padding**: Ensure that the output feature map after the convolution has the same spatial dimensions (i.e., width and height) as the input feature map. This is particularly useful for deep networks, allowing for the design of deeper architectures without worrying about the shrinking size of the feature maps through the layers.


# Convolution as Linear Operator
> [!example] EECS182 Sp23 Disc04 P1
> ![](Convolution_Operation.assets/image-20240401124655464.png)![](Convolution_Operation.assets/image-20240401124702439.png)![](Convolution_Operation.assets/image-20240401130249997.png)![](Convolution_Operation.assets/image-20240401133130845.png)![](Convolution_Operation.assets/image-20240401134110424.png)![](Convolution_Operation.assets/image-20240401133901588.png)![](Convolution_Operation.assets/image-20240401134235407.png)![](Convolution_Operation.assets/image-20240401135336162.png)



















# Convolution Kernels/Filters
## Filter Types
> [!def]
> ![](Convolution_Operation.assets/image-20240328175504013.png)![](Convolution_Operation.assets/image-20240328175509030.png)![](Convolution_Operation.assets/image-20240328175513159.png)![](Convolution_Operation.assets/image-20240328175518832.png)



## Receptive Fields
> [!def]
> ![](Convolution_Operation.assets/image-20240328175556697.png)![](Convolution_Operation.assets/image-20240328175603898.png)![](Convolution_Operation.assets/image-20240328175704108.png)


## Down Sampling
> [!def]
> ![](Convolution_Operation.assets/image-20240328183128298.png)![](Convolution_Operation.assets/image-20240328183135186.png)


### Strided Convolution
> [!def]
> ![](Convolution_Operation.assets/image-20240328175815139.png)![](Convolution_Operation.assets/image-20240401135641389.png)![](Convolution_Operation.assets/image-20240401135806149.png)![](Convolution_Operation.assets/image-20240401140056394.png)





### Pooling
> [!def]
> ![](Convolution_Operation.assets/image-20240328175833823.png)



#### Max Pooling
> [!def]
> ![](Convolution_Operation.assets/image-20240328175854749.png)




#### Average Pooling
> [!def]
> ![](Convolution_Operation.assets/image-20240328175904806.png)



## Example
> [!example]
> ![](Convolution_Operation.assets/image-20240328175950372.png)











