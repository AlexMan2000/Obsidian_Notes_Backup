# Overview
## Goal of the Internet
> [!overview]
> ![](1_Packets&Networks.assets/51370c354beb8117f57ae1cd31b25b2f_MD5.png)
> The main job of the Internet is to transfer data between end hosts. This is more difficult than it seems because there are many considerations:
> - What path do we take between hosts and switches?
> - Do the available paths have adequate bandwidth?
> - What protocols do we use? Can it handle every possible communication case?


## Internet Components
> [!concept]
> At a very high level, the Internet is composed of **three main types of components**:
> 1. **End hosts**, like phones, computers, and IoT devices, send and receive packets as a first or last destination.
> 2. **Switches**, which are often routers, manage the connections between end hosts and forward packets arriving on one link to another link.
> 3. **Links** connect switches and end hosts together. These could be one of many technologies like fiber cables, WiFi, or phone lines.



# Data Organization
## Packets
> [!def]
> ![](1_Packets&Networks.assets/9c95888561075106cd9276cf815de9ef_MD5.png)![](1_Packets&Networks.assets/image-20240223220618472.png)




## Links
> [!def]
> ![image.png](1_Packets&Networks.assets/74d7649dc54b891e2ed0997fbf2e6aad_MD5.png)
> - `Bandwidth`相当于是我的`Packet`传输到网线上所需要的时间。我进门花的时间。
> - `Propagation Delay`相当于我在网线上传输的时间。我在房间里走到目的地花的时间。
> - `BDP`就是长乘宽，相当于容积。



# Packets on Transmission
## Packets on a Link
### TimeLine View
> [!concept]
> **Terminologies:**
> - **Transmission Delay:** Time for a packet to get on/off the wire.
> - **Propagation Delay:** Time for a packet to be transmitted across the link.
> - **Queuing Delay:** Time for a packet to wait until it can be transmitted off the wire by a router. Queuing delay itself doesn't contain the transmission delay.
> - **Packet Delay:** Sum of the above.
> 
> ![image.png](1_Packets&Networks.assets/64c6f60ec9f42a7ec1bbb0664b7a41c0_MD5.png)
> 这个公式可以理解为我上传的时间加上传输的时间，就是我的`Packet Delay`.
> 
> ![](1_Packets&Networks.assets/image-20240223221115462.png)
> 计算方法如下:
> - 10B packet:
> 	- Link 1: $\frac{8\times 10}{10\times 10^{6}}s+10ms=8\times10^{-6}s+10ms=8\times10^{-3}ms+10ms\approx10ms$
> 	- Link 2:$\frac{8\times 10}{1\times 10^{6}}s+10ms=8\times10^{-5}s+1ms\approx1ms$
> - 10000B packet:
> 	- Link 1:$\frac{8\times 10^4}{10\times 10^{6}}s+10ms=8\times10^{-3}s+10ms=8ms+10ms=18ms$
> 	- Link 2: $\frac{8\times 10^4}{1\times 10^{6}}s+10ms=8\times10^{-2}s+1ms=80ms+1ms=81ms$



### Pipe View
> [!concept]
> ![image.png](1_Packets&Networks.assets/33a7b0e0b9ac004e9f5932b7d26433bb_MD5.png)
> Here the first parameter is **bandwidth(bps)**, the second one is **propagation delay(ms)**.
> 
> ![](1_Packets&Networks.assets/image-20240223222129437.png)
> In this representation, the bandwidth is just the width of the link and that the propagation delay is just the length of the link.



### Queuing
> [!def]
> ![](1_Packets&Networks.assets/image-20240224110708409.png)![](1_Packets&Networks.assets/image-20240224110656987.png)![](1_Packets&Networks.assets/image-20240224110634387.png)![](1_Packets&Networks.assets/image-20240224110641470.png)


### Concept Check
> [!example] CS168 Sp24 Disc02 P1
> ![](1_Packets&Networks.assets/image-20240411203336664.png)![](1_Packets&Networks.assets/image-20240411203344405.png)![](1_Packets&Networks.assets/image-20240411204924322.png)






## Packets between Switches/Routers
> [!concept]
> ![image.png](1_Packets&Networks.assets/8dc9d0a0404e8162a56da49cd8c921d9_MD5.png)
> Packet header is useful for those switches to decide how to forward the packets to the desired switches.



## Exercise
> [!example] CS168 Sp24 Disc02 P2
> ![](1_Packets&Networks.assets/image-20240411211110660.png)![](1_Packets&Networks.assets/image-20240411211349098.png)![](1_Packets&Networks.assets/image-20240411211354120.png)![](1_Packets&Networks.assets/image-20240411212132064.png)![](1_Packets&Networks.assets/image-20240411212138756.png)![](1_Packets&Networks.assets/image-20240411212145222.png)![](1_Packets&Networks.assets/image-20240411212152117.png)

















# Challenges
## Addressing and Naming
> [!concept] Important
> ![](1_Packets&Networks.assets/image-20240223222837685.png)![](1_Packets&Networks.assets/image-20240223222908944.png)



## Computing Forwarding Table
> [!def]
> ![image.png](1_Packets&Networks.assets/88b75372941f1b5653acb6674323d82f_MD5.png)![image.png](1_Packets&Networks.assets/7a52706197d12b32fed3e2b66ad0f0d5_MD5.png)
> `Control Plane`就是全局的路径规划算法。
> `Data Plane`就是针对一个`Switch`来说的，下一步去哪里。


### Control Plane Challenges
> [!important]
> ![](1_Packets&Networks.assets/image-20240223223756448.png)




### Data Plane Challenges
> [!important]
> ![](1_Packets&Networks.assets/image-20240223223807631.png)



## Reliable Packet Delivery
> [!important]
> ![](1_Packets&Networks.assets/image-20240224110920835.png)



## Congestion Control
> [!important]
> ![](1_Packets&Networks.assets/image-20240224111111425.png)



# Statistical Multiplexing
## Peak of Demand
> [!def]
> ![](1_Packets&Networks.assets/image-20240223224111425.png)![](1_Packets&Networks.assets/image-20240223225526518.png)
> Peak of aggregate demand means many internet users are trying to access the same resource at the same time and **we assume that the probability of this event is extremely low.** This assumption is the reason why statistical multiplexing works in real life.
> - Here **peak of the aggregate** is obtained by first stacking the function (i.e. $f(x)+g(x)$ pointwise) and find the pointwise maximum to be the value. Like $\max_{x}(f(x)+g(x))$
> - Aggregate of the peak is obtained by first finding the pointwise maximum of each function, then add these maximum. The argmax of different functions could difinitely be very different. Like $\max_{x}f(x)+\max_{x}g(x)$
> 
> This inequality is very much like the Jesen's Inequality.
> 
> ![](1_Packets&Networks.assets/image-20240223225431747.png)![](1_Packets&Networks.assets/image-20240411204757970.png)







## Smooth vs Bursty Applications
> [!def]
> ![](1_Packets&Networks.assets/image-20240224101356093.png)




## Exercise
> [!example] CS168 Sp24 Disc02 P3
> ![](1_Packets&Networks.assets/image-20240411213712831.png)![](1_Packets&Networks.assets/image-20240411213718121.png)![](1_Packets&Networks.assets/image-20240411213724162.png)










# Resource Sharing
## Overview
> [!overview]
> The key question we should ask for statistical multiplexing is that **at what granularity are we multiplexing things.**
> 
> At the granularity of the users of laptops, there is no multiplexing. But at the granularity of the processes and threads inside an OS, there is multiplexing where processes and threads are sharing the CPU and memory resources of the computer.
> ![](1_Packets&Networks.assets/image-20240223230048954.png)![](1_Packets&Networks.assets/image-20240223230113431.png)

> [!important]
> ![](1_Packets&Networks.assets/image-20240223230824180.png)![](1_Packets&Networks.assets/image-20240223230852086.png)



## Circuit Switching
> [!def]
> ![](1_Packets&Networks.assets/image-20240223230549226.png)
> This is like establishing a stable highway(i,e, in terms of transmission speed, determined by the bandwidth  ) between the source and destination before sending any packets of data.
> 
> Note that the bandwidth is guaranteed to be stable once fixed.
> ![](1_Packets&Networks.assets/image-20240411204221593.png)





## Packet Switching
> [!def]
> ![](1_Packets&Networks.assets/image-20240223230752011.png)





## Efficiency
### Multiplexing Granularity
> [!concept] Circuit Switching
> ![](1_Packets&Networks.assets/image-20240224101517567.png)![](1_Packets&Networks.assets/image-20240224100527234.png)![](1_Packets&Networks.assets/image-20240224100536225.png)
> In example 2, only two of three sources will be able to reserve the bandwidth. But any two flows won't use the allocated bandwidth across the entire event(that's why they are bursty), which causes waste in bandwidth reservation.

> [!concept] Packet Switching
> ![](1_Packets&Networks.assets/image-20240224101118300.png)
> Since bandwidth are allocated are packet level instead of flow level, we make more efficient use of bandwidth and get rid of unnecesary reservation of the bandwidth.



### Setup Time
> [!def]
> ![](1_Packets&Networks.assets/image-20240224101751685.png)



## Handling Failures
> [!concept] Circuit Switching
> For circuit switching, when there is network failure, the end host **has to know** whether there is a network failure and then re-setup the reservation and resend the packet flow.
> ![](1_Packets&Networks.assets/image-20240224102825109.png)

> [!concept] Packet Switching
> For packet switching, when the network failure happens, the end host has to do nothing. They **don't have to know** that there is a network failure event.
> ![](1_Packets&Networks.assets/image-20240224102800562.png)


## Complexity of Implementation
> [!concept] Circuit Switching
> ![](1_Packets&Networks.assets/image-20240224103259750.png)
> When we request a reservation from the source to the destination. The general procedure is to find a path from source to destination on which every engaging routers send a "yes" signal to indicate that it is on the reservation path.
> 
> Now in terms of such design, we have to consider the following questions:
> 1. **How do switches know that the reservation went through?**
> If the reservation went through to the destination, then the destination host should send a confirmation message that travels back along the established reservation path to the source and let the routers and source know.
> 2. **What happens if the reservation request is lost mid way?**
> Before a router confirm itself on the reservation path, then it should set up a timer. Before its timeout, it should receive a confirmation message from the successive routers. If yes, then the router know the reservation is established thereafter. If not, then the router knows that the reservation is not successfully established.
> 3. **What happens if the confirmation that the reservation made is lost?**
> One way is the same as above. Another reasonable way is repeatedly send confirmation message from the destination along the reservation path back to the source, in the hope that at least one message will reach the source.


## Summary
> [!summary]
> ![](1_Packets&Networks.assets/image-20240224110116816.png)![](1_Packets&Networks.assets/image-20240224110132246.png)



