# Graph Representation
## Theory
> [!important]
> ![](Graph_Algorithms.assets/image-20240201150906136.png)
> This representation is bad for finding successor for current state, so we typically use adjacency list to represent graph:
> 
> ![](Graph_Algorithms.assets/image-20240201200433175.png)


## Code Implementations
> [!code]
```python
# First, Vertex and Graph classes for directed graphs

class CS161Vertex:
    def __init__(self, v):
        self.inNeighbors = []
        self.outNeighbors = []
        self.value = v
        # useful for DFS
        self.inTime = None
        self.outTime = None
        self.status = "unvisited"
        
    def hasOutNeighbor(self,v):
        if v in self.outNeighbors:
            return True
        return False
        
    def hasInNeighbor(self,v):
        if v in self.inNeighbors:
            return True
        return False
    
    def hasNeighbor(self,v):
        if v in self.inNeighbors or v in self.outNeighbors:
            return True
        return False
    
    def getOutNeighbors(self):
        return self.outNeighbors
    
    def getInNeighbors(self):
        return self.inNeighbors
        
    def addOutNeighbor(self,v):
        self.outNeighbors.append(v)
    
    def addInNeighbor(self,v):
        self.inNeighbors.append(v)
    
    def __str__(self):
        return str(self.value) 
        
# This is a directed graph class for use in CS161.
# It can also be used as an undirected graph by adding edges in both directions.
class CS161Graph:
    def __init__(self):
        self.vertices = []

    def addVertex(self,n):
        self.vertices.append(n)
        
    # add a directed edge from CS161Node u to CS161Node v
    def addDiEdge(self,u,v):
        u.addOutNeighbor(v)
        v.addInNeighbor(u)
        
    # add edges in both directions between u and v
    def addBiEdge(self,u,v):
        self.addDiEdge(u,v)
        self.addDiEdge(v,u)
        
    # get a list of all the directed edges
    # directed edges are a list of two vertices
    def getDirEdges(self):
        ret = []
        for v in self.vertices:
            ret += [ [v, u] for u in v.outNeighbors ]
        return ret
    
    def __str__(self):
        ret = "CS161Graph with:\n"
        ret += "\t Vertices:\n\t"
        for v in self.vertices:
            ret += str(v) + ","
        ret += "\n"
        ret += "\t Edges:\n\t"
        for a,b in self.getDirEdges():
            ret += "(" + str(a) + "," + str(b) + ") "
        ret += "\n"
        return ret
```




# Breadth First Search
## Algorithm
> [!algo]
> ![](Graph_Algorithms.assets/image-20240201200447279.png)

## Runtime Analysis
> [!important]
> ![](Graph_Algorithms.assets/image-20240201200507712.png)![](Graph_Algorithms.assets/image-20240201200512717.png)



## Code Implementations
> [!code]
```python
def BFS(w, G):
    for v in G.vertices:
        v.status = "unvisited"
    n = len(G.vertices)
    Ls = [ [] for i in range(n) ]
    Ls[0] = [w]
    w.status = "visited"
    for i in range(n):
        for u in Ls[i]:
            for v in u.getOutNeighbors():
                if v.status == "unvisited":
                    v.status = "visited"
                    Ls[i+1].append(v)
    return Ls

# This is the graph that was on the slides in class (vertex 1 was Kevin Bacon)
G = CS161Graph()
for i in range(7):
    G.addVertex( CS161Vertex( i ) ) 
V = G.vertices
for pairs in [ (0,2), (0,4), (0, 6), (1, 3), (1, 4), (2, 3), (2, 6), (4, 5), (5,6) ]:
    G.addBiEdge( V[pairs[0]], V[pairs[1]] )
print(G)

levels = BFS(G.vertices[1], G)
for i in range(len(levels)):
    print("Level", i, ":")
    for j in levels[i]:
        print("\t", j)
    
# now what's the distance from node 1 to node 6?
for i in range(len(levels)):
    if G.vertices[6] in levels[i]:
        print("distance from 1 to 6 is", i)
        break
```



## Applications
### Shortest Path - Unweighted
> [!example]
> ![](Graph_Algorithms.assets/image-20240201200534286.png)




# Depth First Search
## Algorithm
> [!algo]
> ![](Graph_Algorithms.assets/image-20240201150656277.png)![](Graph_Algorithms.assets/image-20240201173151170.png)
> Note that for runtime analysis, we have:
> 1. **DFS(...)** visit each vertex once, $O(|V|)$(Outer loop execute V times)
> 2. **DFSVisit(...)** called once per vertex, for each call to the vertex $v\in V$, the runtime is $O(|Adj(v)|)$, so for all the vertices we have $O(\sum\limits_{v\in V}|Adj(v)|)=O(|E|)$ due to handshaking lemma for directed graph.(Sum of the degree is double the cardinality of edges for undirected graph and equal the cardinality fro directed graph).
> 3. In total, we have runtime $O(|V|+|E|)$ and actually $\Theta(|V|+|E|)$

## Edge Classification
> [!important]
> ![](Graph_Algorithms.assets/image-20240201173215997.png)![](Graph_Algorithms.assets/image-20240201195444172.png)
> After executing DFS on graph G, every edge in G can be classified as one of these four edge types. 
> 
> To do this, we need to keep track of when a vertex is first being disocvered (visited) in the search (recorded in start time[v]), and when it is finished (recorded in finish time[v]), that is, when its adjacency list has been examined completely. These timestamps are integers between 1 and 2|V |, since there is one discovery event and one finishing event for each of the |V | vertices.
> 
> **Remarks:**
> 1. **Tree Edges:** Also called parent pointer, if we backtrack the path created by DFS, we can constructed a tree, since each node first visited during DFS has only one parent. 
> 2. **Forward Edges:** An edge pointing from a node to its descent.(Grandchildren). **Detailedly, an edge (u, v) is a forward edge, if v is finished and start time[u] < start time[v].** 
> 3. **Backward Edges:** An edge from a node to its ancestor. (Grandparent)
> 4. **Cross Edges:** An edge pointing from one subtree to another subtree. No hierarchical relationship between. **An edge (u, v) is a cross edge, if v is finished and start time[u] > start time[v]**
> 5. **For undirected graph**, we will never have forward edges, all forward edges will be classified as a backward edges or tree edges, since we can just change the direction and make the starting node being visited by its descent.
> 6. **For undirected graph**, we will never have cross edge, it will be classified as a tree edge or a backward edge.



## DFS Runtime Analysis
> [!important]
> ![](Graph_Algorithms.assets/image-20240201173230190.png)


## Algorithm Implementation
> [!code] 
> ![](Graph_Algorithms.assets/image-20240201195912430.png)![](Graph_Algorithms.assets/image-20240201195923005.png)
```python
def DFS_helper( w, currentTime, verbose ):
    if verbose:
        print("Time", currentTime, ":\t entering", w)
    w.inTime = currentTime
    currentTime += 1
    w.status = "inprogress"
    for v in w.getOutNeighbors():
        if v.status == "unvisited":
            currentTime = DFS_helper(v, currentTime, verbose)
            currentTime += 1
    w.outTime = currentTime
    w.status = "done"
    if verbose:
        print("Time", currentTime, ":\t leaving", w)
    return currentTime
        
def DFS( w, G, verbose=False ):
    for v in G.vertices:
        v.status = "unvisited"
        v.inTime = None
        v.outTime = None
    return DFS_helper( w, 0, verbose )
```



## Applications
> It turns out that we can use the edge type information to perform lots of interesting tasks.
### Cycle Detection
> [!concept]
> ![](Graph_Algorithms.assets/image-20240201200036475.png)![](Graph_Algorithms.assets/image-20240201173305989.png)![](Graph_Algorithms.assets/image-20240201173319827.png)
> The question is: Even is there is a cycle in our directed graph, how do we make sure that the DFS will go through that cycle so that the directed edge $v_k\to v_0$ will be visited?
> 
> The answer is that during DFS, we look for all the neighbors of any particular vertices, so if we start at $v_0$, we will definitely visit $v_1$ during the for loop and so on, so we will definitely visit $v_k$ some time and loop back to $v_0$.
> 
> The key logic is that we can return from the higher level of recursion before we return from the lower level of the recursion. So $v_k$ will visit $v_0$ before $v_0$ finish visiting and $v_0$ won't finish visiting before $v_k$ finish visiting.
> 
> Thus, when we first visit $v_k$, $v_0$ is still on the recursion stack(since it is not finishing visiting), thus $v_0$ is the ancestor of $v_k$ and thus $v_k\to v_0$ is a back edge, which finishes the proof.



### Job Scheduling
> [!concept]
> ![](Graph_Algorithms.assets/image-20240201173411665.png)![](Graph_Algorithms.assets/image-20240201173426403.png)



### Topological Sort
> [!algo]
> ![](Graph_Algorithms.assets/image-20240201200052644.png)![](Graph_Algorithms.assets/image-20240201173439152.png)
> It means, for any node $v$, I will put this node in `order` after I have expanded all its children and descents. In this way, the node that has the most prerequisites will be added first to the order and the starting node will be added last. Then we just reverse the `order` and get the topological sort result.

> [!proof] Correctness
> ![](Graph_Algorithms.assets/image-20240201173448798.png)
> What this tells us is that the nodes that have more edge dependencies will be added to `order` first, so that later on when we do reversion operation, we get the correct topological sort result.

> [!code] Method 1: DFS - Reverse Method
> 
```python
def topologicalSortDFS(graph):
    visited = {}
    recStack = {}
    topoList = []

    for node in graph:
        visited[node] = False
        recStack[node] = False

    for node in graph:
        if not visited[node]:
            if dfsHelper(graph, visited, recStack, topoList, node):
                raise LookupError("Cycle Detected")

    return list(reversed(topoList))


def dfsHelper(graph, visited, recStack, topoList, currNode):
    visited[currNode] = True
    
    # Used for cycle detection
    recStack[currNode] = True

    for successor in graph[currNode]:
        if not visited[successor]:
            if dfsHelper(graph, visited, recStack, topoList, successor):
                return True
        elif recStack[successor]:
            return True

    recStack[currNode] = False
    topoList.append(currNode)
```

> [!code] Method 2: Kahn's Algorithm
```python
def topologicalSortQueue(graph):
    q = queue.Queue()
    topoList = []

    # 1. Find all the nodes that have no incoming edges(source nodes)
    nodeDegreeMap = findDegrees(graph)

    sourceNodes = list(map(lambda elem: elem[0], filter(lambda elem: elem[1]["in"] == 0,nodeDegreeMap.items() )))


    # 2. Put all the souce nodes into the queue
    for node in sourceNodes:
        q.put(node)


    # 3. While the queue is not empty
    while not q.empty():
        # 3.1 Pop the node from the front of the queue
        currNode = q.get()

        # 3.2 Append that source node to the topo ordering list
        topoList.append(currNode)

        # 3.3 For each neighbor of the current node
        for neighbor in graph[currNode]:
            # 3.3.1 Decrease the in degree of this neighbor by one(deleting the incoming edges)
            nodeDegreeMap[neighbor]["in"] -= 1

            # 3.3.2 If the neighbor becomes a source due to 0 in-degree, append it to the queue
            if nodeDegreeMap[neighbor]["in"] == 0:
                q.put(neighbor)


    # 4. Finally, If the length of the topo ordering list is less than the number of nodes,
    # then there is a cycle in the graph and no topological ordering is possible
    # Since if there is a cycle, then the in-degree of the nodes in the cycle will always be
    # bigger than or equal to 1 and there will be no source nodes added to the queue and the
    # while loop is terminated prematurely.
    if len(topoList) < len(graph):
        raise LookupError("Cycle Detected!")

    return topoList


def findDegrees(graph) -> Dict:
    nodeDegreeMap = {}

    for node in graph:
        nodeDegreeMap[node] = {"in": 0, "out": 0}

    for node in graph:
        for neighbor in graph[node]:
            nodeDegreeMap[node]["out"] += 1
            nodeDegreeMap[neighbor]["in"] += 1

    return nodeDegreeMap



if __name__ == "__main__":  
    testGraphMulti = {"A": ["B","C"],  
                  "B": ["C","D","E"],  
                  "C": ["F"],  
                  "D": [],  
                  "E": ["F"],  
                  "F": []}  
  
    testGraphEmpty = {  
  
    }  
  
    testGraphCycle = {  
        "A": ["B", "C"],  
        "B": ["C", "D", "E"],  
        "C": ["D"],  
        "D": [],  
        "E": ["A"]  
    }
```







# Shortest Path Problem(SSSP)
## Problem Definition
> [!def]
> ![](Graph_Algorithms.assets/image-20240201200655272.png)![](Graph_Algorithms.assets/image-20240201201457641.png)![](Graph_Algorithms.assets/image-20240201201504638.png)![](Graph_Algorithms.assets/image-20240201203204483.png)


## Time Complexity
> [!important]
> ![](Graph_Algorithms.assets/image-20240201203431573.png)![](Graph_Algorithms.assets/image-20240201205923922.png)



## Weighted Shortest Path - BFS
> [!important]
> ![](Graph_Algorithms.assets/image-20240201223127217.png)![](Graph_Algorithms.assets/image-20240201223159288.png)


# SCC Problems
## Basic Idea
> [!important]
> ![](Graph_Algorithms.assets/image-20240411164643334.png)![](Graph_Algorithms.assets/image-20240411164652957.png)![](Graph_Algorithms.assets/image-20240411164657310.png)




## Algorithm
> [!algo]
> ![](Graph_Algorithms.assets/image-20240411164843328.png)![](Graph_Algorithms.assets/image-20240411165016943.png)![](Graph_Algorithms.assets/image-20240411165021049.png)




## Example
> [!example]
> ![](Graph_Algorithms.assets/image-20240411170430032.png)![](Graph_Algorithms.assets/image-20240411170423700.png)![](Graph_Algorithms.assets/image-20240411170445798.png)



## Proof of Correctness
> [!proof]
> ![](Graph_Algorithms.assets/image-20240411171034973.png)![](Graph_Algorithms.assets/image-20240411171041891.png)![](Graph_Algorithms.assets/image-20240411171049665.png)![](Graph_Algorithms.assets/image-20240411171054519.png)


## Code Implementations
> [!code]
```python
def DFS_helper( w, currentTime, ordering, verbose ):
    if verbose:
        print("Time", currentTime, ":\t entering", w)
    w.inTime = currentTime
    currentTime += 1
    w.status = "inprogress"
    for v in w.getOutNeighbors():
        if v.status == "unvisited":
            currentTime = DFS_helper(v, currentTime, ordering, verbose)
            currentTime += 1
    w.outTime = currentTime
    w.status = "done"
    ordering.insert(0, w)
    if verbose:
        print("Time", currentTime, ":\t leaving", w)
    return currentTime
       
# This is a version of DFS which outputs vertices in the order that DFS leaves them.
# We used it for topological sorting in Lecture 9
def SCC( G, verbose=False ):
    ordering = []
    for v in G.vertices:
        v.status = "unvisited"
        v.inTime = None
        v.outTime = None
    currentTime = 0
    for w in G.vertices:
        if w.status == "unvisited":
            currentTime = DFS_helper( w, currentTime, ordering, verbose )
        currentTime += 1
    # now reverse all the edges
    E = G.getDirEdges()
    for x,y in E:
        G.reverseEdge(x,y)
   
    # and do it again, but this time in the order "ordering"
    SCCs = []
    for v in ordering:
        v.status = "unvisited"
        v.inTime = None
        v.outTime = None
    currentTime = 0 
    for w in ordering:
        visited = [] 
        if w.status == "unvisited":
            currentTime = DFS_helper( w, currentTime, visited, verbose )
            SCCs.append(visited[:])
        currentTime += 1
    return SCCs


SCCs = SCC(G, False)
for X in SCCs:
    print ([str(x) for x in X])
```



# Useful Lemmas in SSSP
## Subpaths of Shortest Paths 
> [!property]
> ![](Graph_Algorithms.assets/image-20240201203412155.png)![](Graph_Algorithms.assets/image-20240201203418748.png)




## Relaxation Operation is Safe
> [!concept]
> ![](Graph_Algorithms.assets/image-20240201203228883.png)
> The term "safe" in "relaxation is safe" means that performing relaxation operations will not lead to an overestimation or underestimation of the true shortest path distances. 
> 
> It ensures that the algorithm (such as Dijkstra's or Bellman-Ford algorithm) will correctly find the shortest paths, assuming the algorithm's other conditions (such as no negative-weight cycles in the case of Dijkstra's algorithm) are met. 
> 
> This is a fundamental concept ensuring the algorithms' correctness and efficiency in solving shortest path problems.



## Simple Shortest Paths
> [!important]
> ![](Graph_Algorithms.assets/image-20240206232607043.png)


## Negative Edges Detection
> [!important]
> ![](Graph_Algorithms.assets/image-20240201201614074.png)![](Graph_Algorithms.assets/image-20240201201630760.png)


## Negative Cycle Detection
> [!important]
> In graphs where edges can have negative weights, if there is a cycle whose total weight is negative, it's theoretically possible to reduce the path length indefinitely by going around the cycle multiple times. In such a case, the shortest path is undefined because you can always have a shorter path by traversing the negative cycle more times.
> ![](Graph_Algorithms.assets/image-20240206232635182.png)




# SSSP on DAGs
## DAG Relaxation
> [!def]
> ![](Graph_Algorithms.assets/image-20240206231116552.png)


## Algorithm
> [!concept] Shortest Path on DAGs can be solved with TS
> ![](Graph_Algorithms.assets/image-20240206231141484.png)![](Graph_Algorithms.assets/image-20240201204235403.png)![](Graph_Algorithms.assets/image-20240201204336432.png)![](Graph_Algorithms.assets/image-20240201204340381.png)


## Time Complexity
> [!important]
> ![](Graph_Algorithms.assets/image-20240206231203173.png)




# Dijkstra's Algorithm
## Algorithm&Example
> [!algo]
> ![](Graph_Algorithms.assets/image-20240206224829474.png)![](Graph_Algorithms.assets/image-20240201204907676.png)![](Graph_Algorithms.assets/image-20240201204914883.png)


## Dijkstra Complexity
> [!important]
> ![](Graph_Algorithms.assets/image-20240206224920177.png)![](Graph_Algorithms.assets/image-20240206230121037.png)


## Proof of Correctness
> [!proof]
> ![](Graph_Algorithms.assets/image-20240206224659353.png)


## Code Implementations
> [!code]
```python
# make a random graph
# This is G(n,p), where we have n vertices and each (directed) edge is present with probability p.
# if you pass in a set of weights, then the weights are chosen uniformly from that set.
# otherwise all weights are 1
def randomGraph(n,p,wts=[1]):
    G = CS161Graph()
    V = [ CS161Vertex(x) for x in range(n) ]
    for v in V:
        G.addVertex(v)
    for v in V:
        for w in V:
            if v != w:
                if random() < p:
                    G.addDiEdge(v,w,wt=choice(wts))
    return G


# first let's implement this with an array, not a priprity queue
def dijkstraDumb(w,G):
    for v in G.vertices:
        v.estD = math.inf
    w.estD = 0
    unsureVertices = G.vertices[:]
    while len(unsureVertices) > 0:
        # find the u with the minimum estD in the dumbest way possible
        u = None
        minD = math.inf
        for x in unsureVertices:
            if x.estD < minD:
                minD = x.estD
                u = x
        if u == None:
            # then there is nothing more that I can reach
            return
        # update u's neighbors
        for v,wt in u.getOutNeighborsWithWeights():
            if u.estD + wt < v.estD:
                v.estD = u.estD + wt
                v.parent = u
        unsureVertices.remove(u)
    # that's it!  Now each vertex holds estD which is its distance from w

def dijkstraDumb_shortestPaths(w,G):
    dijkstraDumb(w,G)
    # okay, now what are all the shortest paths?
    for v in G.vertices:
        if v.estD == math.inf:
            print("Cannot reach " + str(v))
            continue
        path = []
        current = v
        while current != w:
            path.append(current)
            current = current.parent
        path.append(current)
        path.reverse()
        print([ str(x) for x in path ])


# test on a random graph
G = randomGraph(5,.2)
print(G)
dijkstraDumb_shortestPaths(G.vertices[0], G)




# now let's try this with a heap
def dijkstra(w,G):
    for v in G.vertices:
        v.estD = math.inf
    w.estD = 0
    unsureVertices = heapdict.heapdict()
    for v in G.vertices:
        unsureVertices[v] = v.estD
    while len(unsureVertices) > 0:
        # find the u with the minimum estD, using the heap
        u, dist = unsureVertices.popitem() 
        if u.estD == math.inf:
            # then there is nothing more that I can reach
            return
        # update u's neighbors
        for v,wt in u.getOutNeighborsWithWeights():
            if u.estD + wt < v.estD:
                v.estD = u.estD + wt
                unsureVertices[v] = u.estD + wt #update the key in the heapdict
                v.parent = u
    # that's it!  Now each vertex holds estD which is its distance from w


def dijkstra_shortestPaths(w,G):
    dijkstra(w,G)
    # okay, now what are all the shortest paths?
    for v in G.vertices:
        if v.estD == math.inf:
            print("Cannot reach " + str(v))
            continue
        path = []
        current = v
        while current != w:
            path.append(current)
            current = current.parent
        path.append(current)
        path.reverse()
        print([ str(x) for x in path ])

# test on a random graph
G = randomGraph(5,.4,[1,2,3,4,5])
print(G)
dijkstra_shortestPaths(G.vertices[0], G)
```



# Bellman Ford
> [!algo]
> When there is negative weights edge in the graph, Dijkstra's algorithm won't work. We opt for Bellman Ford if there is no negative cycles.
> ![](Graph_Algorithms.assets/image-20240201205512409.png)![](Graph_Algorithms.assets/image-20240201220524824.png)![](Graph_Algorithms.assets/image-20240214220306784.png)
> Runtime is $\Theta(VE)$.
> 
> Note that if the graph is a DAG, then there is no negative cycles.

> [!thm]
> ![](Graph_Algorithms.assets/image-20240201205607690.png)![](Graph_Algorithms.assets/image-20240201205611408.png)![](Graph_Algorithms.assets/image-20240201210424770.png)

> [!corollary] 
> ![](Graph_Algorithms.assets/image-20240201210404757.png)

> [!bug] Important
> If there is negative cycles, finding shortest path is NP hard.



# LeetCode Problems
## No 547 Number of Provinces
> [!def] 
> ![](Graph_Algorithms.assets/image-20240704152923062.png)

> [!code]
> 由于本题是无向图，于是思路比较简单，就是利用[Depth First Search](Graph_Algorithms.md#Depth%20First%20Search)。每进行一次`DFS`, 看一下是否还有剩余节点， 如果有则说明当前的`DFS`没有覆盖到所有的城市，当前`DFS`的结果记为一个省份， 然后从下一个没有覆盖到的城市开始进行下一次`DFS`。
```java
class Solution {
    public int findCircleNum(int[][] isConnected) {

        int num_cities = isConnected.length;


        int num_province = 0;

        Map<Integer, Boolean> visited = new HashMap<>();

        
        for (int i = 0; i < num_cities; i++) {
            visited.put(i, false);
        }

        for (int i = 0; i < num_cities; i++) {
            if (visited.get(i) == false) {
                num_province++;
                dfs(visited, i, isConnected);
            }
        }
        return num_province;
    }

    public void dfs(Map<Integer, Boolean> visited, int starting_node, int[][] adj_matrix) {
        
        visited.put(starting_node, true);
        List<Integer> successors = findSuccessors(starting_node, adj_matrix, visited);
        if (successors.size() == 0) {
            return;
        }

        for (Integer node: successors) {
            dfs(visited, node, adj_matrix);
        }
    }


    public List<Integer> findSuccessors(int curr_node, int[][] adj_matrix, Map<Integer, Boolean> visited) {

        List<Integer> adj_list = new ArrayList<>();
        for (int i = 0; i < adj_matrix[curr_node].length; i++) {
            if (adj_matrix[curr_node][i] == 1 && visited.get(i) == false) {
                adj_list.add(i);
            }
        }
        return adj_list;
    }

}
```



## No 841 Keys and Rooms
> [!def]
> ![](Graph_Algorithms.assets/image-20240704154031686.png)

> [!code]
> 本题使用拓扑排序比较复杂，用`DFS`即可，只要判断最终`visited`中为`True`的节点数量是否等于房间数即可。
```java
class Solution {

    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
List<Integer> res = new ArrayList<>();

        Map<Integer, Boolean> visited = new HashMap<>();
        Map<Integer, Boolean> recStack = new HashMap<>();

        for (int i = 0; i < rooms.size(); i++) {
            visited.put(i, false);
            recStack.put(i, false);
        }

        dfs(0, rooms, visited, recStack);

        return visited.entrySet()
                    .stream()
                    .filter(elem -> elem.getValue())
                    .map(elem -> elem.getKey())
                    .collect(Collectors.toList())
                    .size()
         == rooms.size();
    }

    public boolean dfs(Integer node
                        , List<List<Integer>> rooms
                        , Map<Integer, Boolean> visited
                        , Map<Integer, Boolean> recStack) {
        visited.put(node, true);

        if (recStack.get(node)) {
            return true;
        }
        recStack.put(node, true);

        List<Integer> neighbors = rooms.get(node);
        for (Integer neighbor: neighbors) {
            if (!visited.get(neighbor)) {
                if (dfs(neighbor, rooms, visited, recStack)) {
                    return true;
                }
            }
            
        }
    
        recStack.put(node, false);
        return false;
    }

}
```





## No 802 Find Eventual Safe States
> [!def] 
> ![](Graph_Algorithms.assets/image-20240704112212044.png)

> [!code]
> 本题的难点在于对于题目的理解，所有的安全节点实际上就是不在环内的节点。因为所有环内的节点的`out degree`总是大于等于`1`。于是在反向图中，所有在环内的节点的`in degree`总是大于等于`1`，于是这些节点在我们的BFS拓扑排序时不会被加入到队列中。
> 
> 思路比较简单，就是现在反向图上做一个[Topological Sort](Graph_Algorithms.md#Topological%20Sort), 然后将得到的拓扑排序进行一个排序即可
```java
class Solution {
    public List<Integer> eventualSafeNodes(int[][] graph) { 

        List<Integer> res = new ArrayList<>();
        Queue<Integer> q = new ArrayDeque<>();


        // 1. Flip the graph
        Map<Integer, List<Integer>> flippedGraph = flipGraph(graph);

		// 2. Calculate the degree info on the flipped graph
        Map<Integer, Map<String, Integer>> degreeInfo = findAllDegrees(flippedGraph);

		// 3. Find all the source nodes
        List<Integer> soucres = degreeInfo.entrySet()
                                        .stream()
                                        .filter(elem -> elem.getValue().get("in") == 0)
                                        .map(elem -> elem.getKey())
                                        .collect(Collectors.toList());

		// 4. Add all the source nodes to the queue
        for (Integer source: soucres) {
            q.add(source);
        }


		// 5. Start the BFS Topological Sorting
        while (!q.isEmpty()) {
            Integer node = q.poll();
            res.add(node);
            for (Integer neighbor: flippedGraph.get(node)) {
                degreeInfo.get(neighbor).put("in", degreeInfo.get(neighbor).get("in") - 1);
                if (degreeInfo.get(neighbor).get("in") == 0) {
                    q.add(neighbor);
                }
            }
        }

		// 6. Collect the results, only those nodes that aren't in the cycle will be defined as safe nodes.
        Collections.sort(res);

        return res;

    }

	/** 
		Functions that flip the graph, from (node, neighbor) to (neighbor, node)
	*/
    public Map<Integer, List<Integer>> flipGraph(int[][] graph) {
        int numNodes = graph.length;
        Map<Integer, List<Integer>> res = new HashMap<>();

        for (int i = 0; i < numNodes; i++) {
            res.put(i, new ArrayList<>());
        }

        for (int i = 0; i < numNodes; i++) {
            for (int neighbor: graph[i]) {
                res.get(neighbor).add(i);
            }
        }

        return res;
    }

	
    public Map<Integer, Map<String, Integer>> findAllDegrees(Map<Integer, List<Integer>> graph) {


        Map<Integer, Map<String, Integer>> nodeDegreeMapping = new HashMap<>();

        // Initialize
        for (Integer i: graph.keySet()) {
            Map<String, Integer> hashMap = new HashMap<>();
            hashMap.put("in", 0);
            hashMap.put("out", 0);
            nodeDegreeMapping.put(i, hashMap);
        }

        // Populate
        for (Integer i: graph.keySet()) {
            for (Integer neighbor: graph.get(i)) {
                 nodeDegreeMapping.get(i).put("out",nodeDegreeMapping.get(i).get("out") + 1 );
                 nodeDegreeMapping.get(neighbor).put("in", nodeDegreeMapping.get(neighbor).get("in") + 1);
            }
        }


        return nodeDegreeMapping;
    }

}
```
 


## No 1129 Shortest Path with Alternating Colors
> [!code]
> ![](Graph_Algorithms.assets/image-20240705203832473.png)
```java

```



