

- [Fill a Special Grid](https://leetcode.com/contest/weekly-contest-448/problems/fill-a-special-grid/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - You are given a non-negative integer N representing a 2N x 2N grid. You must fill the grid with integers from 0 to 2^(2N - 1) to make it special. A grid is special if it satisfies all the following conditions:
		You are given a non-negative integer N representing a 2N x 2N grid. You must fill the grid with integers from 0 to 22N - 1 to make it special. A grid is special if it satisfies all the following conditions:
		
		All numbers in the top-right quadrant are smaller than those in the bottom-right quadrant.
		All numbers in the bottom-right quadrant are smaller than those in the bottom-left quadrant.
		All numbers in the bottom-left quadrant are smaller than those in the top-left quadrant.
		Each of its quadrants is also a special grid.
		Return the special 2^N x 2^N grid.
		
		Note: Any 1x1 grid is special.
		
		 

    ---

    ### 💭 My Initial Thoughts
    - As soon as i saw the problem and i noted down in the paper that in a 4 X 4 cell, the top left is filled , next bottom left, bottom right then top right ( We have to fill in the values from the 2^2N-1 to 0 ,so kept a global variable for it .)
    - Then i intially thought this could be solved via simulation ( iterating ).  When i thought of the case n=3, i got assured that this should be filled using recursion ,as we need to make sure that every quadrant is filled in this way

    ---

    ### ❌ Mistakes Made
    - the mistake that i did was, i did set the end index and start index proper, i did endx//2, which didn't do the correct job. 
    - it didnt consider the local index
    - should have been relative to start
    - Here's the problematic sketch:
      ```python
         def recursivefill(startx,endx,starty,endy,size):
            if(size==2):
                fillquadrant(startx,starty)
                return
            partition=size//2
            #mistake
            recursivefill(startx,endx//2,starty,endy//2,partition)
            recursivefill(endx//2,endx,starty,endy//2,partition)
            recursivefill(endx//2,endx,endy//2,endy,partition)
            recursivefill(startx,endx//2,endy//2,endy,partition)
     
           ```

    ---

    ### ✅ Key Takeaways
    - dry run once

    ---

    ### 🧭 Step-by-Step Approach
    - 
    ---

    ### ✅ Final Code

    ```python
	  class Solution:
    def specialGrid(self, N: int) -> List[List[int]]:
        if(N==0):
            return [[0]]
        self.no=2**(2*N)-1
        n=2**N
        grid=[[0 for _ in range(n)] for _ in range(n)]
        def fillquadrant(startx,starty):
            grid[startx][starty]=self.no
            self.no-=1
            grid[startx+1][starty]=self.no
            self.no-=1
            grid[startx+1][starty+1]=self.no
            self.no-=1
            grid[startx][starty+1]=self.no
            self.no-=1

        def recursivefill(startx,endx,starty,endy,size):
            if(size==2):
                fillquadrant(startx,starty)
                return
            partition=size//2
            #mistake
            # recursivefill(startx,endx//2,starty,endy//2,partition)
            # recursivefill(endx//2,endx,starty,endy//2,partition)
            # recursivefill(endx//2,endx,endy//2,endy,partition)
            # recursivefill(startx,endx//2,endy//2,endy,partition)
            recursivefill(startx, startx + partition, starty, starty + partition, partition)  # top-left
            recursivefill(startx + partition, startx + size, starty, starty + partition, partition)  # top-right
            recursivefill(startx + partition, startx + size, starty + partition, starty + size, partition)  # bottom-right
            recursivefill(startx, startx + partition, starty + partition, starty + size, partition)

        recursivefill(0,n,0,n,n)
        return grid
     
    ```

    ---

    ### ⏱ Time Complexity
    - 4^n

    ### 🗃 Space Complexity
    - 4^n

    ---

    ### 📚 Related Concepts and Topics

