In a simple graph, there is no _(self-)loop_ edge (an edge that connects a vertex with itself) and no _multiple_/_parallel_ edges (edges between the same pair of vertices). In another word: There can only be up to one edge between a pair of distinct vertices.


Graphs are data structures that have a wide-ranging application in real life. These include analysis of electrical circuits, finding the shortest routes between two places, building navigation systems like Google Maps, even social media using graphs to store data about each user, etc.

### **Types of Graphs**

![](https://lh4.googleusercontent.com/tUHFhIbd3F9K3VUOos44xhQkm9C5bPSFqE0YNvb_jA7OyNKoJETnGwqTefsELqG9JBJGXF2E2SEw_XFfvNW_ccXfTMtY3oU2e9C2aJ4tg1d21mZKtNTVyGTxzOh_nH33VyX4tI8_LoyuLk16xh1wLV8)

1. **An undirected graph** is a graph where edges are bidirectional, with no direction associated with them, i.e, there will be an undirected edge. In an undirected graph, the pair of vertices representing any edge is unordered. Thus, the pairs (u, v) and (v, u) represent the same edge.

2. **A directed graph** is a graph where all the edges are directed from one vertex to another, i.e, there will be a directed edge. It contains an ordered pair of vertices. It implies each edge is represented by a directed pair <u, v>. Therefore, <u, v> and <v, u> represent two different edges.

So a graph does not necessarily mean to be an enclosed structure, it can be an open structure as well. A graph is said to have a cycle if it starts from a node and ends at the same node. There can be multiple cycles in a graph.

![](https://lh6.googleusercontent.com/DfrUwFWWXA6dvxsUpgsuPHMkV1tUm_0g8b2IHT-xz3wWsWAv5ho1PWK_qKoy-5fNanrupZqZj5Go058l1xm3i-CCkGbD35EI4LIfAx7sJ0sENXyUKzu9t7BUu3_oqIk9D_4vE7DpwDZiWeParWoUu5s)

If there is at least one cycle present in the graph then it is called an **Undirected Cyclic Graph.**

In the following examples of directed graphs, the first directed graph is not cyclic as we can’t start from a node and end at the same node. Hence it is called **Directed Acyclic Graph,** commonly called **DAG.**

![](https://lh6.googleusercontent.com/vCVUDaBeBU2yQiG_okHHQ8nVs2SnPkIxvlkdzy6HJxgi8rKriovb18x9wonxe7DZCH7rDhRO2KBZ7E8dJNDmXHZJxaIcwFAfDL59Klvo_L0eXJKTTVikWP7AcBl_0rkmj9m87vTqjEXvtwh-8LT-R6Y)

If we just add an edge to the directed graph, then at least one cycle is present in the graph, hence it becomes **Directed Cyclic Graph**.

**Path in a Graph**  ![](https://lh3.googleusercontent.com/DgZLJ9dhn39Y1Mi4lUQTGRFHtWIOq2Dc6vDlAoCr7KG9RgPpIe26dhbdZV3IpvkwrajaXlu1TuTUWa7YRI5OiGDhTqowOkjCLe9qP7bUPW8G4Hqn01DR9SqXr0zMQNj7rA72TEQAz8PFpcA59F65gwc)

The path contains a lot of nodes and each of them is reachable.

is not a path, because a node can’t appear twice in a path.



## Degree of Graph 
It is the number of edges that go inside or outside that node.


## Why is it true for Undirected Graphs?

In an **undirected graph**, each edge connects **two vertices**.

So when you calculate the **degree** of each vertex (number of edges touching that vertex), each edge contributes **+1 to two vertices**.

Hence:
![[Pasted image 20250710101839.png]]


