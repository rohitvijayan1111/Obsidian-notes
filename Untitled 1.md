class Solution:
    def longestSubarray(self, arr, k):
        # Code Here
        n=len(arr)
        prefixsum=0
        first_occurence={}
        max_len=0
        for i in range(n):
            prefixsum+=1 if arr[i]>k else -1
            #since it has nullified all the negative(IF ANY) and now has more >k
            if(prefixsum>0):
                max_len=i+1
            #Checking if the value increased that is 
            #if the prefixsum came from prefix-1 (I.E INCREASED)
            #since there would be always an linear increase
            if(prefixsum-1 in first_occurence):
                max_len=max(max_len,i-first_occurence[prefixsum-1])
            
            if(prefixsum not in first_occurence):
                first_occurence[prefixsum]=i
        return max_len
        
        
        https://www.geeksforgeeks.org/problems/longest-subarray-with-majority-greater-than-k/1