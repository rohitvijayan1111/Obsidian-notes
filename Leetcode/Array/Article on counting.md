Great. I’ll compile a comprehensive guide to counting subarray problems on LeetCode. This will include various categories like fixed sum, product constraints, distinct elements, and sliding window maximums. I’ll also identify the common algorithms and data structures used in solving them (e.g., sliding window, prefix sums, hash maps, two pointers), and provide example problems under each category.

I’ll let you know once the guide is ready.

# Guide to Counting Subarray Problems on LeetCode

Counting subarrays that satisfy certain conditions is a common theme in array problems. These problems often involve constraints on the sum, product, or elements of the subarray. This guide organizes common **subarray-counting problem types**, links representative LeetCode examples, and explains the **optimal approaches** and techniques (prefix sums, hash maps, two pointers/sliding window, binary search, monotonic queues, etc.) used to solve them.

## Common Categories of Subarray-Counting Problems

- **Sum-based subarrays**:
    
    - _Subarrays with sum equal to K_: e.g. [LC 560: Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k) – count subarrays summing to a target.
        
    - _Subarrays with sum divisible by K_: e.g. [LC 974: Subarray Sums Divisible by K](https://leetcode.com/problems/subarray-sums-divisible-by-k) – count subarrays whose sum mod K is 0.
        
    - _Subarrays with sum in a range [L,R]_: e.g. [LC 327: Count of Range Sum](https://leetcode.com/problems/count-of-range-sum) – count sums in [lower, upper].
        
    - _Subarrays with sum ≤ K_ (for non-negative arrays): common technique similar to “at most K” patterns.
        
- **Product-based subarrays**:
    
    - _Subarrays with product less than K_: e.g. [LC 713: Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k) – count contiguous subarrays whose product is < K.
        
- **Distinct-element subarrays**:
    
    - _Subarrays with exactly K distinct elements_: e.g. [LC 992: Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers) – count subarrays with exactly K unique numbers.
        
    - _Subarrays with at most K distinct elements_: often used as a helper (compute exactly K by difference of “at most K” counts).
        
- **Bounded-value subarrays (max/min constraints)**:
    
    - _Subarrays with bounded maximum_: e.g. [LC 795: Number of Subarrays with Bounded Maximum](https://leetcode.com/problems/number-of-subarrays-with-bounded-maximum) – count subarrays whose max element lies in [L,R].
        
    - (Similarly, problems can be posed on the minimum value or on absolute differences, often solved by sliding window + monotonic queues.)
        
- **Bitwise/XOR-based subarrays**:
    
    - _Subarrays with given XOR_: (Not a specific LC example here, but solvable via prefix-XOR + hash map, akin to sum K.)
        
    - _Binary subarrays with sum K_: e.g. [LC 930: Binary Subarrays With Sum] – count subarrays with K ones (sliding window).
        

Below is a table summarizing these types and representative problems:

|**Problem Type**|**Example LeetCode(s)**|**Key Techniques**|
|---|---|---|
|Sum = K|[560](https://leetcode.com/problems/subarray-sum-equals-k)|Prefix-sum + Hash Map (O(N))|
|Sum divisible by K|[974](https://leetcode.com/problems/subarray-sums-divisible-by-k)|Prefix-sum mod + Hash Map (O(N))|
|Range sum [L,R]|[327](https://leetcode.com/problems/count-of-range-sum)|Prefix-sum + Divide & Conquer (O(N log N))|
|Sum ≤ K (all positives)|(No specific LC link)|Sliding Window / Two Pointers (O(N))|
|Product < K|[713](https://leetcode.com/problems/subarray-product-less-than-k)|Sliding Window / Two Pointers (O(N))|
|Exactly K distinct elements|[992](https://leetcode.com/problems/subarrays-with-k-different-integers)|Sliding Window + Counting (O(N))|
|At most K distinct elements|(Helper for above)|Sliding Window (O(N))|
|Bounded maximum (max in [L,R])|[795](https://leetcode.com/problems/number-of-subarrays-with-bounded-maximum)|Two Pointers / Prefix-Count (O(N))|
|Sliding window maximum/minimum (of fixed size)|[239](https://leetcode.com/problems/sliding-window-maximum) (fixed window)|Monotonic Queue (O(N))|

Each of these categories uses one or more **patterns**. The sections below explain the **common techniques** and then detail the **optimal approach** for each category.

## Common Techniques and Patterns

- **Prefix Sum + Hash Map**: Build a running sum (prefix sum) as you iterate. Store counts of each prefix sum (or prefix sum mod K) in a hash map. For each index `i`, if you need a subarray sum (or XOR) equal to `K`, check if `(prefixSum[i] – K)` (or `(prefixXOR[i] ^ K)`) has been seen before. Increment the answer by the count of that value. This yields O(N) solutions for _sum=K_, _sum divisible by K_, and XOR problems. For example, in **Subarray Sum = K** one checks `if currSum - K` exists and adds its count to the result; similarly for **sum divisible by K** one uses `currSum % K` and adds count of the same remainder.
    
- **Sliding Window / Two Pointers**: When the array has only non-negative values (or in some constrained cases), a variable-size sliding window with two indices (`left`, `right`) can count subarrays with sum or product constraints. Expand the right pointer, update the running sum/product, and while a constraint is violated (sum > K or product ≥ K), move the left pointer forward. Each time the window is valid, all subarrays ending at `right` are counted in one go (often adding `(right - left + 1)` to the result). This handles **sum ≤ K** (positive array) and **product < K** cases. For **Subarray Product < K**, for example, we multiply the new element into `product`, then while `product >= k` we divide out `nums[left++]`, and finally we add `right-left+1` to the count.
    
- **Binary Search on Sorted Prefix Sums**: For range-sum counting (e.g. count of sums in [L,R]), one can use prefix sums plus sorting or a balanced tree. As we build prefix array `P`, we need to count, for each new `P[j]`, how many earlier `P[i]` satisfy `lower ≤ P[j]-P[i] ≤ upper`. By sorting the prefix sums seen so far, we can binary-search the valid range of indices for each `j`. This yields an O(N log N) solution (or use a Fenwick tree/BIT or divide-and-conquer merge sort).
    
- **Sliding Window Maximum/Minimum with Monotonic Queue**: When needing the maximum or minimum in a sliding window efficiently (e.g. fixed-size or expanding/contracting window), a monotonic deque is used. It maintains elements in sorted order (increasing or decreasing) so that the window’s max/min is at one end. Each element is enqueued and dequeued at most once, achieving amortized O(N) total time. This technique is often used for subarray problems with constraints on the max or min element (e.g. “max-min ≤ K”). In bounded-maximum problems (like LC 795), one often counts subarrays while ensuring the max stays in range; a monotonic deque can track the current window max in O(1) time per move.
    
- **Counting via Complement (At most vs Exactly K)**: For problems asking “exactly K” (distinct elements, K odds, etc.), a common trick is: _#(at most K) – # (at most K–1) = # (exactly K)_. For instance, to count subarrays with exactly K distinct integers, compute the number of subarrays with **at most K** distinct and subtract those with **at most (K–1)** distinct. Each “at most K” can be done with a sliding window (two pointers) in O(N). This difference trick is detailed in LC 992 solutions.
    

Each category below applies one or more of these techniques optimally.

## Subarrays with Sum = K

**Technique:** Prefix Sum + Hash Map.

For an integer array `nums` and target `K`, we want the count of contiguous subarrays summing to `K`. The optimal O(N) solution uses a running prefix sum and a hash map of counts. As we iterate, maintain `currSum += nums[i]`. We store in a map how many times each prefix sum has occurred. At each index, check if `currSum - K` is in the map; if so, there are that many subarrays ending here with sum = K. Also, if `currSum == K`, that itself is a valid subarray, so increment result. Then increment `map[currSum]`.

```python
count = 0
currSum = 0
prefixCount = {0: 1}
for x in nums:
    currSum += x
    # If currSum-K seen before, add those counts
    if currSum - K in prefixCount:
        count += prefixCount[currSum - K]
    # Record current prefix sum
    prefixCount[currSum] = prefixCount.get(currSum, 0) + 1
```

This uses **hash map** lookups and runs in O(N) time. (See for the hash-map idea.) For example, LeetCode 560 uses this exact strategy.

## Subarrays with Sum Divisible by K

**Technique:** Prefix Sum (mod K) + Hash Map.

Here we count subarrays whose sum is divisible by K. We maintain a running sum modulo K: `r = (r + nums[i] % K + K) % K`. Use a map to count how many times each remainder has occurred. If the current remainder `r` has been seen before (including initial 0), then any previous prefix with the same `r` yields a subarray sum that is a multiple of K. In other words, if two prefix sums have equal remainders modulo K, their difference is divisible by K. The answer increments by the count of `r` seen so far, then we increment `map[r]`.

This also runs in O(N). For example, LeetCode 974 is solved by this method. A concise way:

```python
count = 0
curr = 0
remainders = {0: 1}
for x in nums:
    curr = (curr + x) % K
    # Normalize to positive remainder
    curr = (curr + K) % K
    if curr in remainders:
        count += remainders[curr]
    remainders[curr] = remainders.get(curr, 0) + 1
```

If two prefix sums at indices `i<j` have the same remainder `r`, then `sum(i..j) = (pref[j] - pref[i])` is divisible by K.

## Subarrays with Sum in a Range [L,R] (Count of Range Sum)

**Technique:** Prefix Sums + Divide and Conquer or Binary Search.

Given `nums` and bounds `lower, upper`, count subarrays with sum in [L,R]. Compute the prefix array `P` where `P[i]` = sum of first `i` elements (with `P[0]=0`). A subarray sum from `i` to `j-1` is `P[j] - P[i]`. We need `L ≤ P[j] - P[i] ≤ R`. Rearranged: `P[i]` must lie in `[P[j]-R, P[j]-L]`. Thus for each `j`, we want to count how many earlier `P[i]` fall in a sliding range.

The optimal solution uses a modified merge sort (divide-and-conquer) or a balanced tree / BIT to count these pairs in O(N log N). (Alternatively, one can sort the prefixes and use two pointers or binary search for each `j`.)

The key observation is:

> Define `P[i]=sum(nums[0..i-1])`. Then subarray `(i..j)` sum = `P[j+1] - P[i]`.  
> Count all pairs `(i, j)` with `lower ≤ P[j+1]-P[i] ≤ upper`.

One can implement a merge-sort-based count: sort the prefix array, and as you merge, count how many prefixes fall within the needed offset range. This yields an O(N log N) solution that is optimal for large constraints.

## Subarrays with Sum ≤ K (All Nonnegative)

**Technique:** Sliding Window / Two Pointers.

If all numbers are non-negative, one can count subarrays with sum ≤ K efficiently. Initialize `left=0, currSum=0`. For each `right` index, add `nums[right]` to `currSum`. While `currSum > K` and `left <= right`, subtract `nums[left++]` from `currSum` to shrink the window. At each step, all subarrays ending at `right` with sum ≤ K are those starting between `left` and `right`. Thus add `(right - left + 1)` to the count. This is analogous to the product < K method above, but with addition.

This sliding-window method is O(N) and works only when numbers are non-negative (so sum only increases by moving `right`). It’s a special case of the two-pointer pattern. (For general sums with negatives, one must use prefix-sum+binary-search as above.)

## Subarrays with Product < K

**Technique:** Sliding Window / Two Pointers.

Given `nums` of positive integers and `k`, count contiguous subarrays whose product is less than `k`. Maintain `product = 1`, `left = 0`, and a running count. As you move the right pointer `right` from 0 to n-1, multiply `product *= nums[right]`. Then while `product >= k`, divide out `nums[left]` by doing `product //= nums[left++]`. Now the window `[left..right]` has product < k. All subarrays ending at `right` (with start from `left` to `right`) are valid, so add `(right - left + 1)` to the answer.

```python
count = 0
product = 1
left = 0
for right, val in enumerate(nums):
    product *= val
    while left <= right and product >= k:
        product //= nums[left]
        left += 1
    # All subarrays ending at right with left index in [left..right] are valid
    count += (right - left + 1)
```

This runs in O(N) since each element enters and leaves the window at most once. For example, LC 713 is solved this way.

## Subarrays with Exactly K Distinct Elements

**Technique:** Sliding Window + Count Difference Trick.

To count subarrays with exactly `K` distinct integers, use the “at most K” trick. Define a helper that counts subarrays with at most `X` distinct elements using a sliding window (two pointers) with a frequency map. Let `f(X)` = number of subarrays with at most `X` distinct. Then the answer for **exactly K** is `f(K) – f(K-1)`.

The sliding window for _at most X distinct_ works like this: expand `right`, include `nums[right]` in a counter; if the window has more than X distinct, move `left` until it has ≤ X distinct again. At each step, add `(right - left + 1)` to the running sum for `f(X)`. Then do this process twice and subtract:

```python
def atMostK(nums, K):
    count = 0
    freq = {}
    left = 0
    distinct = 0
    for right, x in enumerate(nums):
        if freq.get(x,0) == 0:
            distinct += 1
        freq[x] = freq.get(x,0) + 1
        while distinct > K:
            freq[nums[left]] -= 1
            if freq[nums[left]] == 0:
                distinct -= 1
            left += 1
        count += (right - left + 1)
    return count

# Exactly K distinct = atMostK(nums,K) - atMostK(nums,K-1)
result = atMostK(nums, K) - atMostK(nums, K-1)
```

This yields O(N) time. The logic and subtraction trick is explained in LC 992. Similarly, this method can count subarrays with exactly K odd numbers or other fixed-count properties by transforming values (odd→1, even→0, for example) and applying the same prefix/hmap or sliding-window trick.

## Subarrays with Bounded Maximum

**Technique:** Two Pointers + Prefix-Count or Monotonic Queue.

For a bound on the maximum element (say we want max in `[L,R]`), a known approach is to count subarrays with max ≤ R minus those with max < L. Define `f(X)` = number of subarrays with all elements ≤ X. We can count `f(X)` by scanning and counting runs of elements ≤ X: whenever an element > X appears, the run resets. In fact, if an index `i` is in a run of length `len`, it contributes `(i - start + 1)` subarrays ending at `i`. The count of subarrays whose max is in [L,R] is `f(R) - f(L-1)`.

Concretely for LC 795, implement a helper `f(X)` (similar to atMostK logic):

```python
def countMaxLEQ(nums, X):
    count = 0
    length = 0
    for x in nums:
        if x <= X:
            length += 1
        else:
            length = 0
        count += length
    return count

result = countMaxLEQ(nums, right) - countMaxLEQ(nums, left-1)
```

This is O(N). The reasoning is shown in LC 795’s solution: subtracting counts removes subarrays whose maximum is too low, leaving exactly those in range.

Monotonic queues could also be used if we needed to dynamically maintain the window’s max in more complex scenarios. In the simple bounding case above, the two-pass subtraction method is enough.

## Sliding Window Maximum/Minimum (Monotonic Queue)

**Technique:** Monotonic Deque.

For problems requiring the max (or min) in every window (often of fixed size _k_), use a deque that keeps candidates in decreasing (or increasing) order. As the window moves, pop from the front if out of range, and pop from back any values smaller than the new entry (for max). The front always has the max. Each element is pushed and popped at most once, yielding O(N) complexity.

While “counting” is less direct here, monotonic queues are a key pattern: e.g. **Sliding Window Maximum** (LC 239) is solved in O(N) by a deque. More generally, if a subarray problem asks about max or min constraints, a monotonic queue or two-pointer window using it will often lead to the answer efficiently.

## Binary Search on Sorted Arrays (Prefix Sums)

**Technique:** Sorted Prefix Sums + Binary Search / BIT.

When input arrays are sorted or when working with prefix sums, binary search can help count qualifying subarrays. For example, after computing all prefix sums `P`, sort them. To count subarrays with sum ≤ K (and non-negative numbers), for each start index you binary-search the farthest end that keeps sum ≤ K. In counting range sums, as noted above, one can binary-search the range `[P[i]+lower, P[i]+upper]` among later prefix sums.

A typical approach for **Count of Range Sum** is to recursively sort and merge prefix sums, counting during merge (O(N log N)). In simpler cases of non-negative arrays, one can just binary-search per prefix sum (O(N log N)). The general idea of using binary search over prefix sums is based on sorting and works in O(N log N).

---

Each of these categories leverages the above techniques. By recognizing the pattern (prefix sum, sliding window, monotonic queue, etc.) and applying the optimal method, you can efficiently solve most subarray-counting problems. The linked LeetCode problems are good practice for each type, and their discussions often outline these strategies as well.

**Sources:** LeetCode problem discussions and algorithm explanations were used to summarize these approaches. Each cited work provides detailed justification for the techniques used.