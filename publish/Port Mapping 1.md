## What is port mapping?
> Port mapping connects a port on your host machine (your computer) to a port inside a [[Container 1]]. It’s like connecting a door in your house to a door in a small house inside it (the container).

### the visualization
![[Pasted image 20250315015306 1.png]]
### So...
here's an example of port mapping in [[Docker 1]]-compose.yaml
```
services:
	app:
		build:
			context: .
			dockerfile: Dockerfile
		ports:
			- "80:8080"
```
##### it means :
all the request from host through [[Port 1|port]] 80 will be pass to [[Port 1|port]] 8080 inside the container, so to access the application inside the container -> i need to request it through port 80.
Because App is [[Port Listening 1|listening]] to [[Port 1]]  8080 ->  all [[Port 1]] 80 request is passed by container to [[Port 1]] 8080.  

	Request (80) -> Docker Host (80) -> Container(8080) -> App