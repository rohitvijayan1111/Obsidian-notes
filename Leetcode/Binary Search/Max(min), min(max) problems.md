
# [Max min Height -Binary search + overlapping interval concept](https://www.geeksforgeeks.org/problems/max-min-height--170647/1)

```
class Solution():
    def maxMinHeight(self, arr, k, w):
        n=len(arr)
        # code here
        def isvalid(height):
            count=0
            additions=[0 for _ in range(n)]
            curr_add=0
            for i in range(n):
                curr_add+=additions[i]
                curr=arr[i]+curr_add
                if(curr<height):
                    need=height-curr
                    count+=need
                    if(count>k):
                        return False
                    curr_add+=need
                    if(i+w<n):
                        additions[i+w]-=need
                
            return True
                
        l=0
        r=max(arr)+k
        ans=-1
        while(l<=r):
            mid=l+(r-l)//2
            if(isvalid(mid)):
                ans=mid
                l=mid+1
            else:
                r=mid-1
        return ans 
```