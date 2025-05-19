# Basics
1. Node :- which hold's data eg:- (1)
    
2. Root :- Where tree start OR top node
    
3. Children :- it is a node of a parent node. E.g :- (2) is a child of node (1)
    
4. Parent :- E.g (1) is parent of node (2) & node (3)
    
5. Siblings :- whose parent is same. E.g (4) & (5) are sibling's because there parent is same i.e. (2)
    
6. Ancestor :- Going up from a child or leaf
    
7. Descendant :- Going down from top root
    
8. Leaf :- is that who don't have any child's E.g (4) & (5) & (6) & (7) are leaf node
    

```sql
Now, What is Binary Tree?
```

A tree is called binary tree if node has zero, one or two children.

We can visualize a binary tree as consisting of root node, left child & right child.

```sql
Types of Binary Trees :-

1. Strict Binary tree
2. Full Binary Tree
3. Complete Binary Tree
4. Skew Binary Tree
```

1. **Strict Binary Tree :-** A binary tree is called strict binary tree if each node has exactly teo children or no children.  
    ![image](https://assets.leetcode.com/users/images/6f7309aa-6534-4ae0-a8ad-5972eda746f2_1645959947.778895.png)
    
2. **Full Binary Tree :-** A binary tree in which each node have two children and all the leaf nodes are on the same level.  
    ![image](https://assets.leetcode.com/users/images/98b57f54-b521-40b0-a67a-89a829684ff8_1645960022.0994654.png)
    
3. **Complete Binary Tree :-** A binary tree in which all the levels are completely filled except possibly the lowest one, which is filled from the left.  
    ![image](https://assets.leetcode.com/users/images/8482807f-10da-4e57-9fd1-ce70427b609d_1645960113.655121.png)
    
4. **Skew Binary Tree :-** A binary tree in which every parent has exactly one child.  
    ![image](https://assets.leetcode.com/users/images/0659d046-e8a3-4056-8096-d3121676e3d4_1645960161.5585117.png)
    

```
Build a tree!!
```

**Let's write a code to build a tree something like this:**  
![image](https://assets.leetcode.com/users/images/4fd86740-daa7-483b-8d4c-51aa4dce06b8_1646051452.4814074.png)

![image](https://assets.leetcode.com/users/images/21186c58-0f5c-46e2-8368-be4d2a5b30c2_1646051175.1480286.png)

**`Let's see how the recursive call is taking place:`**  
![image](https://assets.leetcode.com/users/images/442dc43a-357e-47fa-8831-0e3a6b80fbe8_1646051823.0160375.png)

```rust
Now, you'll say wait "MALIK" we want to print level by level!!
```

I'll say okay, for that we will use `"Level Order Traversal"`!

```sql
L1 -->                     (1)
					     /     \
L2 -->                 (2)     (3)
					 /   \    /   \
L3 -->             (4)   (5) (6)  (7)

Something like this, 
first print level-1
then level-2
finally level-3
```

**`Explanation:-`**

- 1st we put (1) in the queue as it's just a root. After that we put it's child in the queue (2) & (3) & pop (1) from the queue & put into arraylist.
    
- Similarly we put (2) left & right 1st in the queue i.e. (4) & (5) then we put (3) left & right in the queue i.e. (6) & (7)
    
- Now we check for (4) left & right which is null, similar for (5), (6), (7) which are null as well. We pop them from the queue & put into the arraylist.
    
- Time Complexity :- BigO(N)
    
- Space Complexity :- BigO(N)
    

**=>** As you see we traverse Iteratively using Queue & get the answer in our list of arraylist.

![image](https://assets.leetcode.com/users/images/e6f9bce8-3644-4190-a6e9-173fdd1c890b_1646054081.4701512.png)

**`Solution :-`**

```csharp
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        Queue<TreeNode> q = new LinkedList<>();
        
        if(root == null) return res;
        
        q.offer(root);
        
        while(!q.isEmpty()){
            int len = q.size();
            List<Integer> subres = new LinkedList<>();
            
            for(int i = 0; i < len; i++){
                if(q.peek().left != null) q.offer(q.peek().left);
                if(q.peek().right != null) q.offer(q.peek().right);
                
                subres.add(q.poll().val);
            }
            res.add(subres);
        }
        return res;
    }
}
```

**`Time Complexity :-`**

```sql

Access: O(log(n))
Search: O(log(n))
Insert: O(log(n))
Remove: O(log(n))
```

---

---

```
                                                        Traversal Technique
```

---

---

**`So, there are two traversal technique:-`**

- BFS [ Breadth First Search ]
    
- DFS [ Depth First Search ]
    

Let's understand DFS traversal first with an example:

![image](https://assets.leetcode.com/users/images/3ed4c6df-de06-4435-a6a3-66a61fda6628_1646124662.1933947.png)

**InOrder Traversal (left root right)**  
First go to left from the root once you reach the left leaf null, add that into your result then traverse it right and so on.  
From the above tree the traverse we get is :-

```
4 2 5   1   6 3 7
```

**PreOrder Traversal (root left right)**  
First add to the root then go to left from the root once you reach the left leaf null, then traverse it right and so on.  
From the above tree the traverse we get is :-

```
1 2 4   5   3 6 7
```

**PostOrder Traversal (left right root)**  
First go to left from the root once you reach the left leaf null, then traverse it right and once you reach the null of right now add that value into our result.  
From the above tree the traverse we get is :-

```
4 5 2   6   7 3 1
```

```sql
Trick:- In order to remember these 3 order traversal, remember something like this:

**In**Order --> remember like root in b/w left & right

**Pre**Order --> remember like root before 

**Post**Order --> remember like root in the last 
```

Now, let's understand BFS traversal with an example:-

**=>** BFS go level by level

![image](https://assets.leetcode.com/users/images/109ac89c-2ed5-4265-9921-dbd4cde078ec_1646127262.7582123.png)

Output:-

```
1  2  3  4  5  6  7
```

---

---


# Problems

## Preorder Traversal

### With recursion
print(root.data)
fn(root.left)
fn(root.right)
### Without recursion
- basic inference that we need to use an stack

**Root → Left → Right**

To simulate this using a **stack** (LIFO structure), you must:

1. **Print `node.data`** (process the current/root node)
    
2. **Push `node.right`** onto the stack
    
3. **Push `node.left`** onto the stack
    

This way, the **left child is processed before the right child**, which matches preorder logic.

---

### 🔁 Why push right before left?

Because the **stack is Last-In-First-Out**, so the **last pushed node is visited first**.

By pushing the **right child first**, and then the **left child**, the **left child gets processed first** when popped.


# Inorder Traversal

### With recursion
fn(root.left)
print(root.data)
fn(root.right)

### Without recursion - ⭐ important -as logic is different

```
def inorderTraversal(root):
    stack = []
    current = root

    while current is not None or stack:
        # Step 1: Reach the leftmost node of the current node
        while current:
            stack.append(current)
            current = current.left

        # Step 2: Current is None at this point
        current = stack.pop()      # Node to be processed (inorder root)
        print(current.data)        # Step 3: Visit root

        # Step 4: Visit the right subtree
        current = current.right


```

## ✅ Correct Iterative Strategy (with Stack)

### Algorithm:

1. **Use a stack** to simulate the call stack in recursion.
    
2. Start from `root`, and:
    
    - Keep pushing **left children** onto the stack until you hit `None`.
        
3. Then:
    
    - Pop the stack → this gives you the **current root**.
        
    - Process (`print`) it.
        
    - Move to its **right** subtree and repeat the process.


# Postorder - ⭐⭐⭐ 

## Without recursion

``` 
def postorderTraversal(root):
    if root is None:
        return

    stack1 = [root]
    stack2 = []

    while stack1:
        node = stack1.pop()
        stack2.append(node)

        if node.left:
            stack1.append(node.left)
        if node.right:
            stack1.append(node.right)

    # Reverse of Root → Right → Left is Left → Right → Root (postorder)
    while stack2:
        print(stack2.pop().data)

```



# Level order traversal

- Use an deque
- for each level process it and add it's children
 ```
 class Solution:

    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:

        if(not root):

            return

        res=[]

        queue=deque([root])

        while queue:

            level=[]

            n=len(queue)

            for i in range(n):

                z=queue.popleft()

                if(z.left):queue.append(z.left)

                if(z.right):queue.append(z.right)

                level.append(z.val)

            res.append(level)

        return res


```


- [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - Given the `root` of a binary tree, return _its maximum depth_.

	A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

    ---

    ### 💭 My Initial Thoughts
    - Basic recursion, exploring the left and the right subtree and returning the max path

    ---

    ### ❌ Mistakes Made
    - 
    - Here's the problematic sketch:
      ```python
      l = 0
           ```

    ---

    ### ✅ Key Takeaways
    - 

    ---

    ### 🧭 Step-by-Step Approach

    ---

    ### ✅ Final Code

	    ```python
	    # Definition for a binary tree node.
	
	# class TreeNode:
	
	#     def __init__(self, val=0, left=None, right=None):
	
	#         self.val = val
	
	#         self.left = left
	
	#         self.right = right
	
	class Solution:
	
	    def maxDepth(self, root: Optional[TreeNode]) -> int:
	
	        def helper(root):
	
	            if(not root):
	
	                return 0
	
	            left=helper(root.left)
	
	            right=helper(root.right)
	
	            return 1+max(left,right)
	
	        return helper(root)
	     
	    ```
	
	    ---

    ### ⏱ Time Complexity
    - **O(n)** —alll nodes are explored once

    ### 🗃 Space Complexity
    - **O(1)** — constant space; only counters used.

    ---

    ### 📚 Related Concepts and Topics



- [### Mirror Tree](https://www.geeksforgeeks.org/problems/mirror-tree/1)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - Given a binary tree, convert the binary tree to its Mirror tree.

	Mirror of a Binary Tree T is another Binary Tree M(T) with left and right children of all non-leaf nodes interchanged.

    ---

    ### 💭 My Initial Thoughts
    - i could see that we need to just swap the left and the right
    - do recursively and swap it.
    - first swap the bottom level nodes , then swap the higher nodes

    ---

    ### ❌ Mistakes Made
    - 
    - Here's the problematic sketch:
      ```python
      l = 0
           ```

    ---

    ### ✅ Key Takeaways
    - 

    ---

    ### 🧭 Step-by-Step Approach
    - 
    ---

    ### ✅ Final Code

    ```python
    class Solution:
    #Function to convert a binary tree into its mirror tree.
    def mirror(self, root):
        # Code here
        if(not root):
            return
        left=self.mirror(root.left)
        right=self.mirror(root.right)
        root.left=right
        root.right=left
        return root

     
    ```

    ---

    ### ⏱ Time Complexity
    - O(n)	Each node is visited once

    ### 🗃 Space Complexity
    - Space Complexity	O(h)	Due to recursion stack
    - Auxiliary Space	O(h)	Same as space (no extra DS

    ---

    ### 📚 Related Concepts and Topics