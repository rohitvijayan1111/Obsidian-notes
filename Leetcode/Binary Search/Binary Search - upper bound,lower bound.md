
- **[h](l)**  
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    - You are given the head of a linked list. You have to replace all the values of the nodes with the nearest **prime** number. If more than one prime number exists at an equal distance, choose the **smallest** one. Return the **head** of the modified linked list.

		**Examples :**
		
		**Input:** head = 2 → 6 → 10
		**Output:** 2 → 5 → 11

    ---

    ### 💭 My Initial Thoughts
    - initially itself i recollected the prime number tabulation method i learned earlier
    - What i did was brute force and generate prime no from 2 to 10^5
    - Also figured out that this involves Binary Search also
    ---

    ### ❌ Mistakes Made
    - What i did was brute force and generate prime no from 2 to 10^5
    - 
    - Here's the problematic sketch:
      ```python
      - **Hardcoded prime range (`n = 100000`)**:
    
    - This could be **wasteful** for small inputs.
        
    - And **insufficient** for large input values. For example, if `head` contains `99991`, and you need to look for a prime close to `99991`, it’s okay. But what if there's a `100001`? You’ll miss it.
        
- You **don’t scan the list to find the max value**, so your upper bound for the sieve (`n`) is based on a guess (100000), not actual data.
    
- The `findprime()` function:
    
    - Works similarly to the second code’s `find_closest_prime()`, but could be **less readable** because of inline logic and naming.
        
    - Same logic overall, but `n` passed into it is the length of `primearr`, which is less clear than passing the array itself.
           ```

    ---

    ### ✅ Key Takeaways
    - learnt and revised Primenumber tabulation method
    - Got revised on the binary search, lower bound and upper bound

    ---

    ### 🧭 Step-by-Step Approach
    -  Find the maximum element in the list and generate prime number 2*m(maxi)
    - now find the tabulation of primenumbers
    - bisect and find the position of lowerbound of the element
    - check for the edges like what if in the start,end
    - check if r (element smaller than the lower bound) and l(the lower bound) which is nearest to the prime number
    
    ---

    ### ✅ Final Code

    ```python
    """
Definition for singly Link List Node
class Node:
    def __init__(self,x):
        self.val=x
        self.next=None

"""

class Solution:
    def primeList(self, head):
        # Helper to compute all primes up to a certain number using Sieve of Eratosthenes
        def compute_primes(limit):
            primes = [True] * limit
            primes[0] = primes[1] = False
            '''
            - Because any non-prime number ≤ `m` must have a **factor ≤ √m**.
		    - After that, all remaining `True` numbers are automatically prime.
            '''
            for i in range(2, int(limit**0.5) + 1): 
                if primes[i]:
                    for j in range(i * i, limit, i):
                        primes[j] = False
            return [i for i, is_prime in enumerate(primes) if is_prime]

        # Manual binary search to find the closest prime
        def find_closest_prime(primes, target):
            left, right = 0, len(primes) - 1
            while left <= right:
                mid = (left + right) // 2
                if primes[mid] < target:
                    left = mid + 1
                else:
                    right = mid - 1

            # Handle edge cases
            if left >= len(primes):
                return primes[-1]
            if right < 0:
                return primes[0]

            # Compare which prime is closer
            if abs(primes[left] - target) < abs(primes[right] - target):
                return primes[left]
            else:
                x primes[right]

        # Step 1: Find max value in list to determine limit for prime sieve
        temp = head
        max_val = 0
        while temp:
            max_val = max(max_val, temp.val)
            temp = temp.next

        # Step 2: Generate all primes up to about 2 * max_val
        primes = compute_primes(max_val * 2)

        # Step 3: Replace each value in list with nearest prime
        temp = head
        while temp:
            temp.val = find_closest_prime(primes, temp.val)
            temp = temp.next

        return head
     
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** — each element is visited at most twice (once by `r`, once by `l`).
    - 1 + 1/2 + 1/3 + 1/4 + 1/5 + ... ≈ log n
    - ∑ (1/p) for primes p ≤ m ≈ log(log m) (By harmonic- based on some derivation -compex )
    - binary search would n * log(max_val)

    ### 🗃 Space Complexity
    - **O(max_val)+o(n)** — o(maxvalue) to store the prime number computation and o(n) to store the prime no(much lesser tho) :) 
    - > The number of primes less than or equal to `n` (denoted as `π(n)`) is approximately:
    - ```
		

    ---

    ### 📚 Related Concepts and Topics
