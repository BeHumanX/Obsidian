### What is GraphQL?
GraphQL is a new API standard that enables **declarative data fetching** and being used as alternative to **REST API** . GraphQL only expose a **single endpoint** and responds to **queries**

Visualization
![[Pasted image 20250317163318.png]]

#### **GraphQL fetch everything in a single request.**   
Here's and example:
```
query{
	User(id: "er3th438af03j"){
		name
		posts{
			title
		}
		followers(last: 3){
			name
		}
	}
}
```


```
{
	"data": {
		"User": {
			"name": "Mary",
			"posts": [
				{title: "Learn Something useful"},
				{title: "The Something"},
				{title: "Useful Things"}
			],
			"followers":[
				{name: "John"},
				{name: "Alice"},
				{name: "Sarah"}
			]
		}
	}
}
```