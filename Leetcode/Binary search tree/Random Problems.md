
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
