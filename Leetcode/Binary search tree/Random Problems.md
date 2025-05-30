
- ### [Predecessor and Successor](https://www.geeksforgeeks.org/problems/predecessor-and-successor/1)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - You are given root node of the **BST** and an integer **key**. You need to find the in-order **successor** and **predecessor** of the given key. If either predecessor or successor is not found, then set it to **NULL**.

		**Note**:- In an inorder traversal the number just **smaller** than the target is the predecessor and the number just **greater** than the target is the successor.

    ---

    ### 💭 My Initial Thoughts
    - As soon i saw the problem got the thought of storing all the inorder elements in a tree and doing binary search to find the key and return its previous and the next element
    - And also knew that predecessor will the node's left subtree's max (moving to the left and then continously moving right), sucessor will be the node's right subtree smallest value
    - But couldn't think of how to handle edge cases like the key node didn't have the node's left subtree or right subtree

    ---

    ### ❌ Mistakes Made
    -  couldn't think of edge cases like what will the predecessor or sucessor when the corresponding left/ right subtree doesn't exist
    - Here's the problematic sketch:
      ```python
   
			  ```

    ---

    ### ✅ Key Takeaways
    -  While traversing to the find the key element , the element that we come across could be the PREDECESSOR or SUCESSOR , if the corresponding left / right subtree doesn't exist
    - So make sure to consider the nodes that we visit as the predecessor or sucessor correspondingly
    - If the node.data < key   pre=current
    - else node.data > key suc=current
    

    ---

    ### 🧭 Step-by-Step Approach
    -  If the node.data < key   pre=current, move towards the right
    - else node.data > key suc=current, move towards the left
    - else if the current node is the key, check the predecessor and successor in its child
    
    ---

    ### ✅ Final Code

    ```python
	class Solution:
    def findPreSuc(self, root, key):
        # code here
        pre=None
        suc=None
        current=root
        while(current):
            if(current.data==key):
                if(current.left):
                    temp=current.left
                    while(temp.right):
                        temp=temp.right
                    pre=temp
            
                if(current.right):
                    temp=current.right
                    while(temp.left):
                        temp=temp.left
                    suc=temp
                break
                
            elif(current.data<key):
                pre=current
                current=current.right
            
            else:
                suc=current
                current=current.left
        return [pre,suc]
     
    ```

    ---

    ### ⏱ Time Complexity
		
		| Tree Type    | Height `h` | Time Complexity |
		| ------------ | ---------- | --------------- |
		| Balanced BST | `O(log n)` | Fast            |
		| Skewed BST   | `O(n)`     | Slower          |

    ### 🗃 Space Complexity
    - **O(1)**

    ---

    ### 📚 Related Concepts and Topics
		#trees


- [### Print leaf nodes from preorder traversal of BST](https://www.geeksforgeeks.org/problems/print-leaf-nodes-from-preorder-traversal-of-bst2657/1)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - Given a **preorder** traversal of a **BST**, find the **leaf nodes** of the tree without building the tree.

    ---

    ### 💭 My Initial Thoughts
    - did a lot of pen paper work
    - found that ,we need to do similar to constructing an tree
    - the first node (left) is the root of the current, so we need to construct a bst to its left and right from the preorder traversal
    - we iterate from left+1 till right , and check if preorder[i]>preorder[left], if so that is the partitioning element and we name it as mid, THE DEFAULT VALUE OF MID is RIGHT
    - we now recursively construct the left and the right subtree
    - IF RIGHT-left=1 then only its is an root node and we add it to the array

    ---

    ### ❌ Mistakes Made
    - NO
     
    ---

    ### ✅ Key Takeaways
    - try recursion(TO simulate construct of bst from preorder)

    ---

    ### 🧭 Step-by-Step Approach
    - same as intial thought
      
    ---

    ### ✅ Final Code

    ```python
	class Solution:
		def leafNodes(self, preorder):
			# code here
	        res=[]
	        n=len(preorder)
	        def helper(left,right):
	            if(right-left==0):
	                return
	            if(right-left==1):
	                res.append(preorder[left])
	                return
	            mid=right
	            for i in range(left+1,right):
	                if(preorder[i]>preorder[left]):
	                    mid=i
	                    break
	            
	            # print(left,mid,right)
	            helper(left+1,mid)
	            helper(mid,right)
	        
	        helper(0,n)
	        return res
	     
	    ```

    ---

	    

    ---

    ### 📚 Related Concepts and Topics

- ### [Closest Neighbour in BST](https://www.geeksforgeeks.org/problems/closest-neighbor-in-bst/1)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    -  Given the **root** of a **[binary search tree](https://www.geeksforgeeks.org/binary-search-tree-data-structure/ "BST")** and a number **k**, find the greatest number in the binary search tree that is less than or equal to **k**.

    ---

    ### 💭 My Initial Thoughts
    - 

    ---

    ### ❌ Mistakes Made
    -  an optimization code below
    - 
      ```python
	     class Solution:
		    def findMaxFork(self, root, k):
		        def helper(node):
		            if not node:
		                return -1
		            if node.data == k:
		                return node.data
		            elif node.data < k:
		                right_res = helper(node.right)
		                return right_res if right_res != -1 else node.data
		            else:
		                return helper(node.left)
		        
		        return helper(root)

           ```

    ---

    ### ✅ Key Takeaways
    -  We could have done it better by returning the value using recursion itself
    - refer above code

    ---

    ### 🧭 Step-by-Step Approach
	- basic binary search and updating the value of it when it <=k
	
    ---

    ### ✅ Final Code

    ```python
    
		class Solution:
		    def findMaxFork(self, root, k):
		        #code here
		        res=-1
		        def helper(root):
		            nonlocal res
		            if(not root):
		                return
		            if(root.data>k):
		                helper(root.left)
		            elif(root.data<k):
		                res=root.data
		                helper(root.right)
		            else:
		                res=root.data
		                return
		            
		        helper(root)
		        return res
     
    ```

	**Time Complexity: O(h)**
	
	- In the best or average case, the time complexity is **O(log n)** if the BST is balanced.
	    
	- In the worst case, the time complexity is **O(n)** if the BST is skewed (like a linked list).
	    
	
	**Space Complexity: O(h)**
	
	- The space complexity is due to the recursion stack.
	    
	- It will be **O(log n)** for a balanced BST.
	    
	- It will be **O(n)** for a skewed BST.
	### 📚 Related Concepts and Topics
	
	

- ### [2359. Find Closest Node to Given Two Nodes](https://leetcode.com/problems/find-closest-node-to-given-two-nodes/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    -  You are given a **directed** graph of `n` nodes numbered from `0` to `n - 1`, where each node has **at most one** outgoing edge.
		
		The graph is represented with a given **0-indexed** array `edges` of size `n`, indicating that there is a directed edge from node `i` to node `edges[i]`. If there is no outgoing edge from `i`, then `edges[i] == -1`.
		
		You are also given two integers `node1` and `node2`.
		
		Return _the **index** of the node that can be reached from both_ `node1` _and_ `node2`_, such that the **maximum** between the distance from_ `node1` _to that node, and from_ `node2` _to that node is **minimized**_. If there are multiple answers, return the node with the **smallest** index, and if no possible answer exists, return `-1`.
		
		Note that `edges` may contain cycles.

    ---

    ### 💭 My Initial Thoughts
    - spent a lot of time thinking about
    - also thought the "ATMOST ONE OUTGOING EDGE" - would give us a lead
    
    ---

    ### ❌ Mistakes Made
    -  could have done in an optimized way like below 
    - Here's the problematic sketch:
      ```python
		       class Solution:
		    def closestMeetingNode(self, edges: List[int], node1: int, node2: int) -> int:
		        visited1 = set()
		        visited2 = set()
		        while node1 != -1 or node2 != -1:
		            if node1 in visited1:
		                node1 = -1
		            
		            if node2 in visited2:
		                node2 = -1
		
		            if node1 != -1:
		                visited1.add(node1)
		            
		            if node2 != -1:
		                visited2.add(node2)
		
		            if node1 in visited2 and node2 in visited1:
		                return min(node1, node2)
		            
		            if node1 in visited2:
		                return node1
		            
		            if node2 in visited1:
		                return node2
		            
		            if node1 != -1:
		                node1 = edges[node1]
		
		            if node2 != -1:
		                node2 = edges[node2]       
		                 
		        return -1
           ```

    ---

    ### ✅ Key Takeaways
    -  need to explore more
    - they had only asked for the node
    - so could have just done using the set,like which every node is visits the node of the other, then that would be node to be returned

    ---

    ### 🧭 Step-by-Step Approach
	- I did dfs and calculated the distance to reach each node from node1 and stored it
	- similarly an dfs , from node2 and if the node is visited by the node1 then the max of the two distance is taken into consideration
	
    ---

    ### ✅ Final Code

    ```python
		class Solution:
	
	    def closestMeetingNode(self, edges: List[int], node1: int, node2: int) -> int:
	
	        n=len(edges)
	
	        dist={}
	
	        visited=[False for _ in range(n)]
	
	        def dfs(ind,c):
	
	            visited[ind]=True
	
	            dist[ind]=c
	
	            if(edges[ind]!=-1 and not visited[edges[ind]] ):
	
	                dfs(edges[ind],c+1)
	
	        dfs(node1,0)
	
	        self.mini=float("inf")
	
	        self.node=-1
	
	        visited=[False for _ in range(n)]
	
	        def dfs2(ind,c):
	
	            visited[ind]=True
	
	            if(ind in dist):
	
	                comp=max(c,dist[ind])
	
	                if(comp<self.mini):
	
	                    self.mini=comp
	
	                    self.node=ind
	
	                elif(comp==self.mini):
	
	                    self.node=min(self.node,ind)
	
	            if(edges[ind]!=-1 and not visited[edges[ind]]):
	
	                dfs2(edges[ind],c+1)
	
	        dfs2(node2,0)
	
	        return self.node if self.mini!=float("inf") else -1
	     
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** 

    ### 🗃 Space Complexity
    - **O(n)**

    ---

    ### 📚 Related Concepts and Topics

