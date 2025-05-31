
# return -1

```python
'''
class Node:
    def __init__(self, val, k):
        self.right = None
        self.data = val
        self.left = None
'''
class Solution:
    # returns the inorder successor of the Node x in BST (rooted at 'root')
    def inorderSuccessor(self, root, x):
        # Code here
        
        if(not root):
            return -1
        if(root.data==x.data):
            temp=root.right
            while(temp and temp.left):
                temp=temp.left
            return (temp and temp.data) or -1
        elif(root.data>x.data):
            res=self.inorderSuccessor(root.left,x)
            return res if res!=-1 else root.data
        else:
            return self.inorderSuccessor(root.right,x)
        
```


# Stack to simulate an recursion

