
- Horizontal scaling 
- vertical scaling


# DNS Server

- this could also help traffic equally

LOAD Balancing

- could split traffic based on cpu usage
- or dedicate some service to a instance and traffic all the request to it accordingly 




HOW WOULD TRAFFIC THE USER TO THE SAME INSTANCE VIA THE LOAD BALANCER:

ISSUE: the user might need to login again and again , as the session cookie might not be stored in the other instances. OR The user might have added the things to carts in one instance , some in the other, this becomes difficult 


SOLUTION:
- Storing it in the load balancer itself or somewhere else
- COULD ASSIGN RANDOM ID TO THE SERVER AND STORE IT IN THE COOKIE OF THE USER, THE LOADBALANCER WILL DIRECT THE TRAFFIC TO THE RIGHT USER , BASED ON THE ID
  

SUPPOSE THE ELB IS THE ONE STORING EVERTHING = HOW DO WE ENSURE THE DATA ISNT LOST
RAID
RAID1
RAID5
RAID6
RAID10




CACHING


- MY SQL QUERY CACHE ->
- MEMCACHE->


WHAT TO DO IF THE CACHE IS GETTING FULL
- TRY TO DISCARD THE ONE THAT IS OLD AND LESS RECENTLY USED



DATABASE REPLICATION:

- HAVE ONE MASTER AND CREATE REPLICA OF THE SLAVES
- so an write query hits the master, it is copied down to all others
- so thereby IT CAN BE USED AS A LOAD BALANCING FOR READ REQUEST



- USE TWO MASTER SERVERS


![[Pasted image 20250606211531.png]]


WHAT IF THE LOAD BALANCER DIES (SINGLE POINT OF FAILURE)


ADD EXTRA LOAD BALANCER AND PARTITION 

![[Pasted image 20250606212843.png]]




- That leads to the first golden rule for scalability: every server contains exactly the same codebase and does not store any user-related data, like sessions or profile pictures, on local disc or memory.   
  
Sessions need to be stored in a centralized data store which is accessible to all your application servers. It can be an external database or an external persistent cache, like Redis. An external persistent cache will have better performance than an external database. By external I mean that the data store does not reside on the application servers. Instead, it is somewhere in or near the data center of your application servers.