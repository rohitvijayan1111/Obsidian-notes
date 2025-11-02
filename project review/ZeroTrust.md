
* Z3r0Trust, an autonomous middleware leveraging Descope to protect enterprise systems and third-party applications from brute-force attacks, credential abuse, and malicious API usage. Implemented real-time log intelligence, continuous authentication, and automated anomaly response (blocking users), reducing SOC analyst workload by 70% while maintaining analyst oversight for false positives.
* Our problem statement was to create an solution that involved secure communication between Agents using Descope .


Our solution:

* when an application enrolls with us an middleware , what happen is we give a proxy url for frontend to call the backend.
* Therefore we can log all the request going to the backend server.

AGENTS INVOLVED:

1. Log Detection Agent:
2. Analyst agent
3. Alert handler agent
4. DB controller agent
5. Mail Handler agent
6. Appeal handler agent


## *Log Detection Agent*

* The log detection agent does nothing but ingests all the request from the frontend and forwards the request to splunk 
* Created an endpoint to ingest data into splunk easily


