
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
  
  
RAID

RAID0
RAID1