
- Horizontal scaling
- vertical scaling
- processing using cron jobs
- using backup servers
- Microservices
- Distributed systems
- Load balancing 
- Decoupling 
- Logging and metrics
- Extensible 



#### Self hosting

![[Pasted image 20250515161542.png]]

We need to take into consideration , like what if there is a power loss



#### Cloud hosting

![[Pasted image 20250515161621.png]]



#### The server that you have is not capable of handling those many request what do we do?

![[Pasted image 20250515161739.png]]

> ANSWER : SCALABILITY 

##### OPTION 1 : BUY MORE MACHINE : HORIZONTAL SCALING


##### Option 2: BUY BIGGER MACHINE: VERTICAL SCALING



#### COMPARISON


| Criteria             | Horizontal                                                                                                                          | Vertical                                                                              |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Load Balancing       | Possible                                                                                                                            | Not possible                                                                          |
| Single point failure | Resilient                                                                                                                           | Single point of failure                                                               |
| Communication        | Happens over the network(So might be slow)- Remote procedural calls                                                                 | Happens via Inter process communication                                               |
| Data consistency     | Difficult to maintain consistency (Inconsistent - might need to lock all the server when such things happen to maintain uniformity) | It is easy to maintain consistency as it is an single system                          |
| Scalability          | Scales well, as user increase                                                                                                       | there is a hardware limit /  threshold beyond which it can't be scaled up vertically. |


Summary :
Issues based on horizontal and vertical scaling.

Horizontal Scaliing (Multiple servers)
1. Load Balancing Required
2. Resilient
3. Network call (RPC - Remote Procedure Call)
4. Data Inconsistency
5. Scales well as users increase

Vertical Scaliing (Single server)
1. N/A
2. Single point of failure
3. Inter process communication
4. Consistent
5. Hardware Limit