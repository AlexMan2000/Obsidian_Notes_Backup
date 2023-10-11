# Capacitor
## Definition
> ![](1_Capacitors.assets/image-20230318182625389.png)


## Current of Capacitor
> ![](1_Capacitors.assets/image-20230318182724947.png)![](1_Capacitors.assets/image-20230318182742590.png)



## Voltage of Capacitor
> 🔔: 由于$V_C$是以$\frac{dV_C}{dt}$的形式存在的，所以我们需要对两边求积分来求解。
> ![](1_Capacitors.assets/image-20230318182930018.png)![](1_Capacitors.assets/image-20230318182939540.png)
> ❗: 所以我们看到，如果我们对电容充电的话，最终电容两端的电压$V_C$（电容器上下板的电荷会越来越多）会不断增大，最终可能烧掉电容器。
> 🔔: 现实生活中，电容的一个典型的例子是积雨云，当云中的电荷量积累到一定程度时，就会通过闪电的方式进行放电。




# Capacitor Physics
## Physical Structure
> ![](1_Capacitors.assets/image-20230318211748336.png)![](1_Capacitors.assets/image-20230318212613762.png)

>[!info] Physical Expression
> ![](1_Capacitors.assets/image-20230318211910711.png)![](1_Capacitors.assets/image-20230318211929472.png)




## Energy Storation - Battery
> ![](1_Capacitors.assets/image-20230318211831085.png)![](1_Capacitors.assets/image-20230318212013409.png)
> 🔔: 当我们在充满`Capacitor`之后把电压源去掉之后，电荷不会凭空消失。这意味着，电容可以用来长时间储存电荷，也就是说，电容可以用于构造电池。





# Circuit with Capacitors
##  Capacitor with Current Source
> ![](1_Capacitors.assets/image-20230318194623125.png)
> 🔔: 在连接`Current Source`充电时，如果充电相同的时间，电容值越大，电压上升速率越小，最终的电压越小，但是储存的电荷量相同。
> 🔔: 另一种更有实际意义的解读是，更大的电容储存相同的电量时只需要更小的电压来维持。




## Capacitor with Voltage Source
> ![](1_Capacitors.assets/image-20230318193139727.png)![](1_Capacitors.assets/image-20230318194843383.png)
> 🔔: 如果`Capacitors`两端连接到$V_S$的话，那么最终电容器两端的电压最多不能超过$V_S$。
> 🔔: 在连接`Voltage Source`充电时，如果充电相同的时间，电容值越大，能够储存的电荷量越多。

 

# Capacitor Equivalence
## Algorithm
> ![](1_Capacitors.assets/image-20230318195531672.png)![](1_Capacitors.assets/image-20230318195512199.png)


## Capacitor in series
### Thevenin/Norton Perspective
> ![](1_Capacitors.assets/image-20230318200622083.png)
> ⭐串联的电容中，$C_{eq}$携带的电荷量和$C_1,C_2$各自携带的电荷量一致，也就是$Q_{C_{eq}}=Q_{C_1}=Q_{C_2}$



### Physical Perspective
> ![](1_Capacitors.assets/image-20230318212508954.png)![](1_Capacitors.assets/image-20230318212517962.png)






## Capacitor in parallel
### Thevenin/Norton Perspective
> ![](1_Capacitors.assets/image-20230318200605752.png)


### Physical Perspective
> ![](1_Capacitors.assets/image-20230318212446237.png)![](1_Capacitors.assets/image-20230318212455432.png)






## Example
> ![](1_Capacitors.assets/image-20230318200738612.png)



# Resistors and Capacitors
> ![](1_Capacitors.assets/image-20230318200754784.png)





# Resources
> [Note16](Typed_Notes/Note16.pdf)
> [Written_Notes16](Typed_Notes/Written_Notes16.pdf)
> https://www.bilibili.com/video/BV1wi4y1u7gx?p=17&vd_source=66aa12d38833505f6c2216f089511404 (Lecture 17)
> https://www.bilibili.com/video/BV1wi4y1u7gx?p=18&vd_source=66aa12d38833505f6c2216f089511404 (Lecture 18)


