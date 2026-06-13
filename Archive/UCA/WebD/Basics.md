- Use LTS version of Node JS 
- A single entity can be client as well as server based on situation.
	- Suppose a client request some service from a server and that server is not self sufficient to process that request , it may need to fetch data from another server (database) so at that situation server makes a request so that's a client behavior at that scenario.
- Server is  user centric.
- Basic requirements that a server has to fulfill is to receive request and provide services.
	- Requirements are:
		- Listening Mode (always active)
		- Processing Data
		- Business Logic
		- Connectivity
		- A running process
- What happens when we start a server ?
	- It starts a process like node js etc. and starts listening mode. 
- In what cases database activates can stop or database goes down?
- What will you check if database is down?
	- Try to connect it with server

- We are never going to use EJS in modern development as it is decrypted and old technology.
- On server HTML also runs to perform server side rendering.
- In banking apps data is controlled based on user but in case of selling products online there is no limit.
	- In case of products every user is source of data.
	- In case of banking app , source of data is bank itself.
- In case source of data is not defined at that is where unstructured data is used and NoSQL database(like MongoDB) is needed. Like on google anyone can search anything and in any language and this kind of thing cannot be fulfilled by SQL database. In most of times you will work on SQL database but in case of product companies like google you may have to work on unstructured data as well.


# Nodemon
- Installed it globally using `npm i -g nodemon`


# Install pm2 for load balancing
- [[About pm2]]
- Using it we can create a cluster which is basically group of processes.
- pm2 manages  the redirection of request from main ip to new ip assigned with different port numbers and it manages the those port numbers as well.
![[Pasted image 20250802111047.png]]

![[Pasted image 20250802111137.png]]

![[Pasted image 20250802111214.png]]

![[Pasted image 20250802111305.png]]


![[Pasted image 20250802111530.png]]


If you are hitting the website multiple time like maybe many users accessing it then it will automatically balance the load by like creating multiple dynamic port address

![[Pasted image 20250802112127.png]]
![[Pasted image 20250802113038.png]]

