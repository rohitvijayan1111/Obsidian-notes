	
- [ ] **Implement LRU Cache**
	- [ ] What did I learn
		- I learnt that doubly linked should also be created with dummy nodes to handle edges cases easily
		- We need to think in terms of function like add, remove and use it every where and code it later
	- [ ] what did i do wrong
		- i did it in an complicated way , i didnt use dummy nodes, didnt use modular functions


- [ ] LFU Cache
	- [ ] what did i Learn
		- I learnt that even if we are using doubly linked list, we need not link all the different frequency together, have it independent  
	- [ ] what did i do wrong
		-  I made small implementations mistakes, like didnt update the minimum frequency to 1 when new node was inserted and also made some small mistake in updating the minimum frequency, when the frequency of the node increased


- [ ] The Celebrity Problem
	- [ ] what did i Learn
		- Learnt that we could find the answer by using two pointer and reducing the search space. instead of iterating through the 2D matrix
	- [ ] what did i do wrong
		-  Initially thought o(n^2) solution is not possible later, discovered that if l->r l cant be a celebrity and if l->r=0 that means r cant be celebrity as we well
		- so start from l=0 r=n-1 and check if l->r is 1 if so increment l else decrement r
		- then do an iteration when l=r to check if it is truly a celebrity 



- [ ] Online stock Span
	- [ ] what did i Learn
		- Check if <= must be put in the monotonic stack checking condition . The problem was simple using the pge was able to find easily the last smaller element
		  
	- [ ] what did i do wrong
		- missed adding <=. the problem was simple and intutive 

