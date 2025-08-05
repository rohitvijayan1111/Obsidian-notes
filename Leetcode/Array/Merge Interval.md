
- ## Intuition

The intuition behind the solution comes from two realizations:

1. If we sort the intervals based on their start times, any overlapping intervals will be placed next to each other in the list.
2. To merge intervals, we only need to track the end time since the sorted order ensures that the next interval's start time is always greater than or equal to the current interval's start time.

The approach is as follows:

1. Sort the list of intervals based on their start times.
2. Initialize a new list to hold the merged intervals and add the first interval to it.
3. Iterate through the rest of the intervals, and for each one, compare its start time with the end time of the last interval in the merged list.
4. If the start time is greater than the end time of the last interval in the merged list, then there is no overlap, and we can add the current interval as a new entry to the merged list.
5. If there is overlap (the start time is less than or equal to the end time), we update the end time of the last interval in the merged list to be the maximum of the end times of the last interval and the current interval.
6. The process continues until we have gone through all the intervals.
7. We return the merged list of intervals as the answer.

This solution guarantees that we merge all overlapping intervals and result in a list of intervals with no overlaps.


# [57. Insert Interval](https://leetcode.com/problems/insert-interval/)

```
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        #TWO CASES:
        #i)the interval is overlapping with any of the current interval
        #ii)the interval is not overlapping ->what if before start ot at the end
        #iii)after inserting/,erging need to check if further it can be merged or not
        res = []
        inserted = False

        for interval in intervals:
            # Case 1: current interval is before newInterval
            if interval[1]<newInterval[0]:
                res.append(interval)
            # Case 2: current interval is after newInterval
            elif interval[0]>newInterval[1]:
                if not inserted:
                    res.append(newInterval)
                    inserted=True
                res.append(interval)
            # Case 3: Overlapping intervals – merge
            else:
                newInterval[0]=min(newInterval[0],interval[0])
                newInterval[1]=max(newInterval[1],interval[1])
        
        # If newInterval not inserted yet 
        if not inserted:
            res.append(newInterval)
        
        return res
```


