
>**Inference**: In graph traversal, if all edge weights are equal (e.g., weight = 1), we can mark a node as visited when it's added to the queue (BFS). However, if edge weights vary (as in Dijkstra's algorithm), we must mark a node as visited only when it is popped from the priority queue to ensure the shortest path is correctly computed.


- [3341. Find Minimum Time to Reach Last Room I](https://leetcode.com/problems/find-minimum-time-to-reach-last-room-i/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - There is a dungeon with `n x m` rooms arranged as a grid.
	
	You are given a 2D array `moveTime` of size `n x m`, where `moveTime[i][j]` represents the **minimum** time in seconds when you can **start moving** to that room. You start from the room `(0, 0)` at time `t = 0` and can move to an **adjacent** room. Moving between adjacent rooms takes _exactly_ one second.
	
	Return the **minimum** time to reach the room `(n - 1, m - 1)`.
	
	Two rooms are **adjacent** if they share a common wall, either _horizontally_ or _vertically_.

    ---

    ### 💭 My Initial Thoughts
    -  As soon i saw this problem got the approach to do with BFS+ priority Queue(heap)

    ---

    ### ❌ Mistakes Made
    - The mistake i did was i restricted future visiting of shorter path,by marking the node visited as soon i added to the priority Queue
    - IT SHOULD NOT BE DONE AND SHOULD BE DONE ONLY WHEN VISITED
    - dont add the next_time (i,e the time that position grid will be open)
    - Here's the problematic sketch:
      ```python
      import heapq

class Solution:

    def minTimeToReach(self, moveTime: List[List[int]]) -> int:

        n,m=len(moveTime),len(moveTime[0])

        visited=[[False for _ in range(m)] for _ in range(n)]

        nextrooms=[]

        currtime=0

        res=0

        #nexttime,curr_time,x,y

        heapq.heappush(nextrooms,(0,0,0))

        directions=[(0,1),(1,0),(-1,0),(0,-1)]

        while nextrooms:

            time,posx,posy=heapq.heappop(nextrooms)

            #exploring  the next move options

            #MISSED TO CHECK THE VISITED HERE

            if(visited[posx][posy]):

                continue

            visited[posx][posy]=True

            if(posx==n-1 and posy==m-1):

                return time

            for i,j in directions:

                nx,ny=posx+i,posy+j

                if(0<=nx<n and 0<=ny<m and visited[nx][ny]==False):

                    #visited[nx][ny]=True -MISTAKE only make it when pop, so that shortest path are explored

                    heapq.heappush(nextrooms,(max(moveTime[nx][ny],time)+1,nx,ny))

        return -1
           ```

    ---

    ### ✅ Key Takeaways
    - use BFS +priority queue

    ---

    ### 🧭 Step-by-Step Approach
    - 
    ---

    ### ✅ Final Code

    ```python
    class Solution:
     
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** — each element is visited at most twice (once by `r`, once by `l`).

    ### 🗃 Space Complexity
    - **O(1)** — constant space; only counters used.

    ---

    ### 📚 Related Concepts and Topics