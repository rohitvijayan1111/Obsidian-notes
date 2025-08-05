
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