
- **[838. Push Dominoes](https://leetcode.com/problems/push-dominoes/)**  
    
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
    - As soon as i saw the problem , i thought of BFS, and a very minute thought of sliding for two pointer
    - Then i came out tried to implement the BFS solution, like simulating the moves in directions

    ---

    ### ❌ Mistakes Made
    - 
    - Here's the problematic sketch:
      ```python
      The mistake i did was , i initially started with count of timer (bfs count), but later thought it was unecessary.

should have maintain an Time array and force(direction) array to store the states
           ```

    ---

    ### ✅ Key Takeaways
    - should have maintain an Time array and force(direction) array to store the states
    - if would be easy to check in it like check is the Time is None (meaning a . node)
    - then we explore it and set the directions
    - then we check if again reach the same node within the current time time=t+1 and and forces are opp
    - then we set it to '.'

    ---

    ### 🧭 Step-by-Step Approach
    - 
    ---

    ### ✅ Final Code method 1

    ```python
     edge case that i need to consider is how am i going to handle two directional fall at the same time

        n=len(dominoes)

        time=[None]*n

        force=[None]*n

        q=deque()

  

        for i, ch in enumerate(dominoes):

            if ch in 'LR':

                q.append((i,0,ch))

                time[i]=0

                force[i]=ch

  

        dominoes =list(dominoes)

  

        while q:

            i,t,d =q.popleft()

            ni=i+1 if d=='R' else i - 1

  

            if 0<=ni<n:

                if time[ni] is None:

                    time[ni]=t+1

                    force[ni]=d

                    q.append((ni,t+1,d))

                elif time[ni]==t+1 and force[ni]!=d:

                    # Collision — cancel out

                    force[ni]='.'

  

        for i in range(n):

            if force[i]!=None and  force[i] in 'LR':

                dominoes[i]=force[i]

  

        return ''.join(dominoes)
    ```

    ### ✅ Final Code method 2 - Two pointer

    ```python
    class Solution:
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
    - **O(2n)** — constant space; only counters used.

    ---

    ### 📚 Related Concepts and Topics