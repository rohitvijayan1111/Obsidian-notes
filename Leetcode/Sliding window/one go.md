
# resources

- https://medium.com/@yourstudybuddy/10-sliding-window-leetcode-problems-that-make-you-understand-better-341c5ca3fbd
- https://medium.com/@rishu__2701/mastering-sliding-window-techniques-48f819194fd7


# NEED TO SOLVE THIS

- https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/description/
- 
# Fixed window



- ### [1876. Substrings of Size Three with Distinct Characters](https://leetcode.com/problems/substrings-of-size-three-with-distinct-characters/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    -  A string is good if there are no repeated characters.

	Given a string s​​​​​, return the number of good substrings of length three in s​​​​​​.
	
	Note that if there are multiple occurrences of the same substring, every occurrence should be counted.
	
	A substring is a contiguous sequence of characters in a string.

    ---

    ### 💭 My Initial Thoughts
    - 

    ---

    ### ❌ Mistakes Made


	---

    ### ✅ Key Takeaways
    - 

    ---

    ### 🧭 Step-by-Step Approach
    - just maintain a sliding of 3 
    ---

    ### ✅ Final Code

    ```python
	    class Solution:
	    def countGoodSubstrings(self, s: str) -> int:
	        count = 0
	        for i in range(len(s) - 2):
	            window = s[i:i+3]
	            if len(set(window)) == 3:
	                count += 1
	        return count
	     
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** 
    ### 🗃 Space Complexity
    - **O(1)**
    
    ---

    ### 📚 Related Concepts and Topics




- ### [643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    -  You are given an integer array `nums` consisting of `n` elements, and an integer `k`.
	
	Find a contiguous subarray whose **length is equal to** `k` that has the maximum average value and return _this value_. Any answer with a calculation error less than `10-5` will be accepted.

    ---

    ### 💭 My Initial Thoughts
    - 

    ---

    ### ❌ Mistakes Made
    
    ---

    ### ✅ Key Takeaways
    - 

    ---

    ### 🧭 Step-by-Step Approach
    - just a template 
    ---

    ### ✅ Final Code

    ```python
	class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        maxi=-float("inf")
        sums=0
        l=0
        n=len(nums)
        for r in range(n):
            if(r-l+1<k):
                sums+=nums[r]
            else:
                sums+=nums[r]
                maxi=max(maxi,round(sums/k,5))
                sums-=nums[l]
                l+=1
        return maxi     
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** 

    ### 🗃 Space Complexity
    - **O(1)** 

    ---

    ### 📚 Related Concepts and Topics



- ### [1461. Check If a String Contains All Binary Codes of Size K](https://leetcode.com/problems/check-if-a-string-contains-all-binary-codes-of-size-k/)
    
    ---

    ### 🧾 Problem Summary (What is given and what is needed?) 
    -  Given a binary string `s` and an integer `k`, return `true` _if every binary code of length_ `k` _is a substring of_ `s`. Otherwise, return `false`.

    ---

    ### 💭 My Initial Thoughts
    - heheh boi , i could think of the permutations problem, to get the no of possible binary variations of length k

    ---

    ### ❌ Mistakes Made
    
    ---

    ### ✅ Key Takeaways
    -  just add the lengths of k strings into the set
    - and verify if the lengths are equal

    ---

    ### 🧭 Step-by-Step Approach
     - 
	
    ---

    ### ✅ Final Code

    ```python
	    class Solution:
    def hasAllCodes(self, s: str, k: int) -> bool:
        st=set()
        n=len(s)
        target=pow(2,k)
        for i in range(n-k+1):
            st.add(s[i:i+k])
            if(len(st)==(target)):
                return True
        return False  
    ```

    ---

    ### ⏱ Time Complexity
    - **O(n)** 

    ### 🗃 Space Complexity
    - **O(1)** 

    ---

    ### 📚 Related Concepts and Topics


## [1343. Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold](https://leetcode.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold/)

```
class Solution:
    def numOfSubarrays(self, arr: List[int], k: int, threshold: int) -> int:
        c=0
        sums=0
        l=0
        n=len(arr)
        for r in range(n):
            if(r-l+1<k):
                sums+=arr[r]
            else:
                sums+=arr[r]
                maxi=round(sums/k,5)
                if(maxi>=threshold):
                    c+=1
                sums-=arr[l]
                l+=1
        return c

```


## [1461. Check If a String Contains All Binary Codes of Size K](https://leetcode.com/problems/check-if-a-string-contains-all-binary-codes-of-size-k/)


```
class Solution:
    def hasAllCodes(self, s: str, k: int) -> bool:
        st=set()
        n=len(s)
        target=pow(2,k)
        for i in range(n-k+1):
            st.add(s[i:i+k])
            if(len(st)==(target)):
                return True
        return False


```


## [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

```
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        d2={}
        for i in p:
            d2[i]=d2.get(i,0)+1
        
        d1={}
        n=len(s)
        l=0
        ind=[]
        for r in range(n):
            d1[s[r]]=d1.get(s[r],0)+1
            if r>=len(p):
                d1[s[l]]-=1
                if d1[s[l]]==0:
                    del d1[s[l]]
                l+=1
            if d1==d2:
                ind.append(l)
        return ind
```


## [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)


```
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        d2={}
        for i in s1:
            d2[i]=d2.get(i,0)+1
        
        d1={}
        n=len(s2)
        l=0
        for r in range(n):
            d1[s2[r]]=d1.get(s2[r],0)+1
            if r>=len(s1):
                d1[s2[l]]-=1
                if d1[s2[l]]==0:
                    del d1[s2[l]]
                l+=1
            if d1==d2:
                return True
        return False
```


## [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/) 🚨
### Description
 We use an monotonic queue concepts for these kind of problems where we need the maximum or minimum element in the each window
### Steps
1) For Maximum element 
	1) We maintain the Queue in the decreasing order
	2) So in each window we take the element from the left of the deque and return it
	3) Before doing so we first check if the first element in the queue is still inbound of the window , if not remove it
	4) now we need to ensure that the current element is positioned currently in the queue
	5) so what we do is continously pop from the right end (No longer needed as the current element in greater than this ) and add the element to the queue once we achieve the right position
 2) for the minimum element
	 1) We maintain the Queue in the increasing order

### Code

```
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        q=deque()
        n=len(nums)
        ans=[]
        for i in range(n):
            if(q and q[0]<i-k+1):
                q.popleft()
            while(q and nums[q[-1]]<=nums[i]):
                q.pop()
            q.append(i)
            if(i>=k-1):
                ans.append(nums[q[0]])
        return ans
```






# Varied 

## [1248. Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/) 🚨

### Description 

**Inclusion Exclusion algo** in this problem they ask to find exactly k odd no in the subarray 
so if using simple sliding window all we can do is to count only some of it.

We can find this by doing atmost k- atmost k-1 element

```
class Solution:
    def numberOfSubarrays(self, nums: List[int], k: int) -> int:
        def helper(k):
            count=0
            n=len(nums)
            odd=0
            l=0
            for r in range(n):
                if(nums[r]%2!=0):
                    odd+=1
                while odd>k:
                    if(nums[l]%2!=0):
                        odd-=1
                    l+=1
                #the no of subarray that could be made from
                count+=(r-l+1)
            return count
        return helper(k)-helper(k-1)
                
```


## [904. Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)

### Description 
It is similar to maximum k different element in an window


```
class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        d={}
        maxi=0
        l=0
        n=len(fruits)
        for r in range(n):
            d[fruits[r]]=d.get(fruits[r],0)+1
            while(len(d)>2):
                d[fruits[l]]-=1
                if(d[fruits[l]]==0):
                    del d[fruits[l]]
                l+=1
            if(len(d)<=2):
                maxi=max(r-l+1,maxi)
        return maxi
```



## [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

```
class Solution:
    def longestOnes(self, nums: List[int], k: int) -> int:
        l=0
        ml=0
        temp=k
        for r in range(len(nums)):
            if(nums[r]==0):
                if(k):  
                    k=k-1
                else:
                    #print("in@",l,r)
                    while(not k):
                        if(nums[l]==0):
                            k=k+1
                        l=l+1
                    k=k-1
                    #print(l,r)
            #print(l,r)
            ml=max(ml,r-l+1)
        return ml
```


## [713. Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)


```
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        if(k==0 or k==1):
            return 0
        l=0
        prod=1
        n=len(nums)
        count=0
        for r in range(n):
            prod=prod*nums[r]
            while(l<n and prod>=k):
                prod=prod//nums[l]
                l+=1
            # print(r-l+1)
            count+=(r-l+1)

        return count

```


## [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)


```
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        l=0
        n=len(nums)
        mini=n
        Flag=True
        total=0
        for r in range(n):
            total+=nums[r]
            while(total>=target):
                mini=min(mini,r-l+1)
                Flag=False
                total-=nums[l]
                l+=1

        return 0 if Flag else mini
```


## [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        l=0
        r=0
        subset=set()
        ml=0
        for r in range(len(s)):
            while(s[r] in subset):
                subset.remove(s[l])
                l=l+1
            subset.add(s[r])
            ml=max(ml,r-l+1)
        return ml
```


## [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/) 🚨


```
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        l=0
        ml=0
        d={}
        for r in range(len(s)):
            d[s[r]]=d.get(s[r],0)+1
           # print(d)
            while(((r-l+1)-max(d.values()))>k):
                #print("IN",r)
                d[s[l]]-=1
                l+=1
                
                #print("IN",d)
            ml=max(ml,r-l+1)
            print(l)
        return ml
        
```



# [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

```
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        l=0
        n=len(s)
        d={}
        dt={}
        ind=[0,0]
        mini=float("inf")
        for i in t:
            dt[i]=dt.get(i,0)+1
        need=len(dt)
        have=0
        for r in range(n):
            if(s[r] in dt):
                d[s[r]]=d.get(s[r],0)+1
                if(d[s[r]]==dt[s[r]]):
                    have+=1
            #But d can have more than dt ->but should be allowed
            while(have==need):
                if(r-l+1<mini):
                    mini=r-l+1
                    ind=[l,r]
                if(s[l] in dt):
                    d[s[l]]-=1
                    if(d[s[l]]<dt[s[l]]):
                        have-=1
                l+=1
        return s[ind[0]:ind[1]+1] if mini!=float("inf") else ""

```


