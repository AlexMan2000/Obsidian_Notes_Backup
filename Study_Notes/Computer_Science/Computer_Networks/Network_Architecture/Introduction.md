# Overview
## Goal of the Internet
> ![](Introduction.assets/51370c354beb8117f57ae1cd31b25b2f_MD5.png)
> The main job of the Internet is to transfer data between end hosts. This is more difficult than it seems because there are many considerations:
> - What path do we take between hosts and switches?
> - Do the available paths have adequate bandwidth?
> - What protocols do we use? Can it handle every possible communication case?


## Internet Components
> At a very high level, the Internet is composed of** three main types of components**:
> 1. **End hosts**, like phones, computers, and IoT devices, send and receive packets as a first or last destination.
> 2. **Switches**, which are often routers, manage the connections between end hosts and forward packets arriving on one link to another link.
> 3. **Links **connect switches and end hosts together. These could be one of many technologies like fiber cables, WiFi, or phone lines.



# Data Organization
## Packets
> ![](Introduction.assets/9c95888561075106cd9276cf815de9ef_MD5.png)


## Links
> ![image.png](Introduction.assets/74d7649dc54b891e2ed0997fbf2e6aad_MD5.png)
> `Bandwidth`相当于是我的`Packet`传输到网线上所需要的时间。我进门花的时间。
> `Propagation Delay`相当于我在网线上传输的时间。我在房间里走到目的地花的时间。
> `BDP`就是长乘宽，相当于容积。




# Packets on a Link
## TimeLine View
> ![image.png](Introduction.assets/64c6f60ec9f42a7ec1bbb0664b7a41c0_MD5.png)



## Pipe View
> ![image.png](Introduction.assets/33a7b0e0b9ac004e9f5932b7d26433bb_MD5.png)



# Packets between Switches
> ![image.png](Introduction.assets/8dc9d0a0404e8162a56da49cd8c921d9_MD5.png)



# Routing
## Definition
> ![image.png](Introduction.assets/88b75372941f1b5653acb6674323d82f_MD5.png)


## Forwarding Table
> ![image.png](Introduction.assets/7a52706197d12b32fed3e2b66ad0f0d5_MD5.png)
> `Control Plane`就是全局的路径规划算法。
> `Data Plane`就是针对一个`Switch`来说的，下一步去哪里。

