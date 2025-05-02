
**GENERAL LEARNINGS :**
1. Monotonic stacks can be used in problems that involves in finding the minimum and maximum of an element



### Problem list:

#### 1. Next Greatest Element  
🔗 [Leetcode – Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/)

- [ ] What did I learn
	- **For Greatest Element → Use Decreasing Monotonic Stack**
	- Learnt that this problem can be solved in two ways:
	  - **Forward Traversal**  
	    - In forward traversal, NGE occurs when the current element is greater than the top of the stack.  
	    - Pop all smaller elements from the stack — those elements have found their "next greater."
	  - **Backward Traversal**  
		  - Traverse left to right.
		  - While stack not empty and curr > stack.top → NGE[stack.top] = curr, then pop.
		  - Push curr index to stack.
	
- [ ] Where did I go wrong

