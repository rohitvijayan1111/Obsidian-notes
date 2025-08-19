
# 1) Chained (a.k.a. Service Chaining / Request Chaining)

## Intent

Compose a response by passing a request **sequentially** through multiple services. Each service does a step (validate → enrich → compute → format), and the final service returns the response.

`Client → S1 → S2 → S3 → (response)`

## Typical Flow

1. **S1** receives the client request; does its work; calls **S2**.
    
2. **S2** processes; calls **S3**.
    
3. **S3** completes and returns the final response upstream to the client.
4. ![[Pasted image 20250819211847.png]]
5. 