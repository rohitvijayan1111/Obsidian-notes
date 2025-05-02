
- [Sort a linked list of 0s, 1s and 2s][] [🔗](https://www.geeksforgeeks.org/problems/given-a-linked-list-of-0s-1s-and-2s-sort-it/1)
    
    - Problem Summary (What is given and what is needed?) #flashcards/leetcode/Linkedlist
	        - Given the **head** of a linked list where nodes can contain values **0s**, **1s,** and **2s** only. Your task is to **rearrange** the list so that all **0s** appear at the beginning, followed by all **1s**, and all **2s** are placed at the end :: [Answer](obsidian://open?vault=Obsidian%20Vault&file=Leetcode/[Category]/[Problem Title])
            
    - My Initial Thoughts
        
        - as soon as i saw this problem i remembered and recalled the dutch national flag algorithm .
            
    - Mistakes Made
        
        - But since this is a singly linked list moving the r pointer (prev element) to the left isnt possible. SO THIS APPROACH DOESNT WORK
        - Came up with an approach of creating 3 dummy header for 0,1,2 and added to it.
        - So in the above approach after iterating through the arr and creating separate list, made mistake in merging .(MISSED THE CONDITION LIKE WHAT IF 1 is not present at all )
             
    - Step-by-Step Approach
        
        - Created 3 header , add 0,1,2 to each and merge it later
        
    - Time Complexity Analysis
        
        - O(N)
    - Space Complexity Analysis
        
        - O(1) since 3 dummy nodes created
            
- **[Find length of Loop](https://www.geeksforgeeks.org/problems/find-length-of-loop/1)**  
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - Given the head of a linked list, determine whether the list contains a loop. If a loop is present, **return the number of nodes** in the loop, otherwise **return 0**.

    ---

    ### 💭 My Initial Thoughts
    - I thought that we could do this using floyd algorithm.


    ---

    ### ❌ Mistakes Made
    - Also did an wrong code
    -     But i did floyd's start of loop like moving the one pointer to the start and doing so 
      ```python
       slow=head
        fast=head
        while(fast and slow!=fast):
            slow=slow.next
            fast=fast.next
            if(fast):
                fast=fast.next
        slow=head
        c=0
        while(slow!=fast):
            slow=slow.next
            fast=fast.next
            c+=1
        return c
           ```

    ---

    ### ✅ Key Takeaways
    - think twice and do the coding

    ---

    ### 🧭 Step-by-Step Approach
    - 
    ---

    ### ✅ Final Code

    ```python
    def counter(node):
            c=1
            nxt=node.next
            while(node!=nxt):
                nxt=nxt.next
                c+=1
            return c
            
        slow=head
        fast=head
        while(fast and fast.next):
            slow=slow.next
            fast=fast.next
            if(fast):
                fast=fast.next
            if(slow==fast):
                return counter(slow)
        return 0
     
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** — each element is visited at most twice (once by `r`, once by `l`).

    ### 🗃 Space Complexity
    - **O(1)** — constant space; only counters used.

    ---

    ### 📚 Related Concepts and Topics

	