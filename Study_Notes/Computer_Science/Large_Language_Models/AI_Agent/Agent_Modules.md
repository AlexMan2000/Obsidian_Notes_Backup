# 四大模块总括
https://lilianweng.github.io/posts/2023-06-23-agent/

> [!def]
> ![](Agent_Modules.assets/eaf27b420baa0a1032585a5dbc8847a6_MD5.jpeg)![](Agent_Modules.assets/c59cb88d9fc66b2af472a519193ce271_MD5.jpeg)




## Memory 模块
> [!def]
> ![](Agent_Modules.assets/df89a3bc00a557413da3e5fc0aa0d9f6_MD5.jpeg)
> - **Short-term memory:** I would consider all the in-context learning as utilizing short-term memory of the model to learn.
> - **Long-term memory:** This provides the agent with the capability to retain and recall (infinite) information over extended periods, often by leveraging an external vector store and fast retrieval.




## Tools 模块
> [!def]
> ![](Agent_Modules.assets/e443406f8a96c603bbdb0d168c855826_MD5.jpeg)
> - The agent learns to call external APIs for extra information that is missing from the model weights (often hard to change after pre-training), including current information, code execution capability, access to proprietary information sources and more.



## Planning 模块
> [!def]
> ![](Agent_Modules.assets/b2bf8ce34894683f762ea16131dfb896_MD5.jpeg)
> - **Subgoal and decomposition:** The agent breaks down large tasks into smaller, manageable subgoals, enabling efficient handling of complex tasks.
> - **Reflection and refinement:** The agent can do self-criticism and self-reflection over past actions, learn from mistakes and refine them for future steps, thereby improving the quality of final results.



## Action 模块
> [!def]
> ![](Agent_Modules.assets/ac612ae8decc9b01dade7baa3c9981ba_MD5.jpeg)




# Planning


