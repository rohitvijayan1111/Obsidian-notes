
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

