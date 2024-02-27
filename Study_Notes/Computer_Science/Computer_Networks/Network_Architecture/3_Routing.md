# Routers
## Why Routers?
> [!important]
> Without routers, when we add new customers to the network, we will have to connect it to all the other customers. As the following picture shows, every time we add a new customer to the network, we have to add $n$ links to the rest of them.
> ![](3_Routing.assets/image-20240226211348254.png)
> We want to have alternative when there is network failures. As the following pictures show, when one connection fails, it should not interfere with the connection between other clients and should be able to qucikly find an alternative path for the current connection.
> 
> ![](3_Routing.assets/image-20240226211534695.png)![](3_Routing.assets/image-20240226211543131.png)


## Challenges of Routing
> [!def]
> ![](3_Routing.assets/image-20240226211127285.png)



## Challenges of Forwarding
> [!def]
> ![](3_Routing.assets/image-20240226211611172.png)



## Routing and Forwarding
> [!important]
> ![](3_Routing.assets/image-20240226211721871.png)![](3_Routing.assets/image-20240226211638837.png)



# Validity of Routing State
## Delivery Tree
> [!def]
> To model a packet delivery event, we use some concepts from graph topology.
> For destination-based routing, we define its `delivery tree` to have the following properties:
> 1. The set of all paths create `directed delivery tree`. The paths must together **cover every node** since we want to be able to reach the destination from any node.
> 2. Each node has only **one outgoing** arrow. 
> 3. Once paths **meet**, they **never split**.
> 4. It is a **spanning tree** since the paths cover all the nodes. We call it an oriented spanning tree rooted at the destination.
> 5. There is **no cycles** in it since it is a tree.
> 
> ![](3_Routing.assets/image-20240226212921693.png)


## Routing State Validity
> [!def]
> - **Local routing state** is table in a single router.
> 	- By itself, the state in a single router can’t be evaluated for validity.
> 	- It must be evaluated in terms of the global context.
> - **Global state** is collection of tables in all routers.
> 	- Global state determines which paths packets take.
> 	- It’s **valid** if it produces forwarding decisions that **always** deliver packets to their destinations
> - Global routing state is valid **if and only if**:
> 	- For **each destination**, there are **no dead ends and no loops** 
> 	- A **dead end** is when there is no outgoing link (next-hop)
> 		- A packet arrives, but is not forwarded (e.g., because there’s no table entry for destination)
> 		- The destination doesn’t forward, but doesn’t count as a dead end!
> 		- But other hosts generally are dead ends, since hosts don’t generally forward packets
> 	- A **loop** is when a packet cycles around the same set of nodes
> 		- If forwarding is deterministic and only depends on destination field, this will go on indefinitely
> - **Necessity:** If there is dead ends or loops, then the forwarding decision will not always deliver packets to their destination, which makes perfect sense.
> - **Sufficiency:** If there is no dead ends and no loops, the forwarding decision will always deliver packets to their destination.
> 	- Packet can't hit the same node twice(no loops).
> 	- Packet can't stop before hitting destination(no dead ends).
> 	- So packets must keep wandering the networj, hitting different nodes
> 		- Only a finite number of unique nodes to visit.
> 		- Must eventually hit the destination.



## Verifying Routing State Validity
> [!def]
> ![](3_Routing.assets/image-20240226215728420.png)![](3_Routing.assets/image-20240226220750994.png)

> [!example] Valid Example
> ![](3_Routing.assets/image-20240226215756642.png)![](3_Routing.assets/image-20240226215822031.png)![](3_Routing.assets/image-20240226215829186.png)![](3_Routing.assets/image-20240226215840136.png)

> [!example] Invalid Example
> ![](3_Routing.assets/image-20240226215911740.png)![](3_Routing.assets/image-20240226215921218.png)![](3_Routing.assets/image-20240226220443126.png)![](3_Routing.assets/image-20240226220636014.png)













