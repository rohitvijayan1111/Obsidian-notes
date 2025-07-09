
# [1353. Maximum Number of Events That Can Be Attended](https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended/)

i tried with arrays but mised edge case

```
class Solution:
    def maxEvents(self, events: List[List[int]]) -> int:
        #Sorting based on the start time
        #be greedy attend the meeting as soon and possible and leave immediately if another meeting starts
        # events.sort(key=lambda x:(x[0],x[1]))
        # count=0
        # nextattend=0
        # for i,j in events:
        #     if(nextattend<i or i<=nextattend<=j):
        #         count+=1
        #         nextattend=max(i+1,nextattend+1)
        #     else:
        #         print("iN ",nextattend,i,j)
        # return count

        events.sort()
        heap=[]
        count=0
        day=0
        ind=0
        n=len(events)
        while ind<n or heap:
            if(not heap):
                day=events[ind][0]
                                            #add to the heap the events that are <=day
            while(ind<n and events[ind][0]<=day):
                heapq.heappush(heap,events[ind][1])
                ind+=1
            
            #remove the ones that are expired
            while heap and heap[0]<day:
                heapq.heappop(heap)
            
            #remove one element
            if heap:
                count+=1
                day+=1
                heapq.heappop(heap)
            else:
                if(ind<n):
                    day=events[ind][0]

            
        return count
```