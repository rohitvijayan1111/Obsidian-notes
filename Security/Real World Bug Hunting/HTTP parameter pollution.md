
- HTTP parameter pollution is a type of attack where we try to modify the parameters of the HTTP request to get unexpected response (trying to break the normal functionality)

- There are two types
	- Client side
	- Server side

## Server side:

- in server side HPP, we can only view the info you send and the response that the server gives, you can't view the servers source code
- The attack can be done, by adding additional parameter , or same parameters repeated(so that the program, if mis configured would take the wrong value)