
- **[h](l)**  
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - There are `n` dominoes in a line, and we place each domino vertically upright. In the beginning, we simultaneously push some of the dominoes either to the left or to the right.

	After each second, each domino that is falling to the left pushes the adjacent domino on the left. Similarly, the dominoes falling to the right push their adjacent dominoes standing on the right.
	
	When a vertical domino has dominoes falling on it from both sides, it stays still due to the balance of the forces.
	
	For the purposes of this question, we will consider that a falling domino expends no additional force to a falling or already fallen domino.
	
	You are given a string `dominoes` representing the initial state where:
	
	- `dominoes[i] = 'L'`, if the `ith` domino has been pushed to the left,
	- `dominoes[i] = 'R'`, if the `ith` domino has been pushed to the right, and
	- `dominoes[i] = '.'`, if the `ith` domino has not been pushed.
	
	Return _a string representing the final state_.

    ---

    ### 💭 My Initial Thoughts
    - did BFS first,later came to know this problem can be done in two pointer

    ---

    ### ❌ Mistakes Made
    - 
    - Here's the problematic sketch:
      ```python
      l = 0
           ```

    ---

    ### ✅ Key Takeaways
    - on observing there are these case:
    - if the first non '.' is L: then the element to the left of it are 'L'
    - if the last non '.' is R: then the element to right of it are 'R'
    - Various cases :
	    - LR- Left Right : no changes would happen
	    - RL- Right Left: equal no of R and L , move pointers equally while "l<r"
	    - LL- makes everything LL
	    - RR- makes them RR
	    
    ---

    ### 🧭 Step-by-Step Approach
    - 
    ---

    ### ✅ Final Code

    ```python
	 class Solution:

    def pushDominoes(self, dominoes: str) -> str:
        l=0

        r=0

        n=len(dominoes)

        domino=list(dominoes)

            if(domino[i]!='.'):

                l=i

                if(domino[i]=='L'):

                    domino[0:i]='L'

        while(r<n):

            #find l

            while(l<n and domino[l]!='.'):

                l=i

                r=i+1

                if(l==0 and domino[i]=='L'):

                    domino[0:i]='L'

            #find r

  

            while(r<n and domino[r]!='.'):

                l=i

                if(l==0 and domino[i]=='L'):

                    domino[0:i]='L'

        if(nums[r])
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** — each element is visited at most twice (once by `r`, once by `l`).

    ### 🗃 Space Complexity
    - **O(1)** — constant space; only counters used.

    ---

    ### 📚 Related Concepts and Topics