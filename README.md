mongoose2pojo
=============

Converts MongooseJS schemas to POJO (Plain Old Java Object)

## Using as library

```JS
var Schema = require("mongoose").Schema;
var m2p = require("mongoose2pojo");
var converter = m2p({
  className: "User"
});
var javaCodeString = converter.parse({
  name: String,
  login: { type: String, required: true },
  registeredBy: { type: Schema.ObjectId, ref: 'User', index: true }
});
```

The resulting `javaCodeString` is:
```java
public class User{
	private String name;
	private String login;
	private UUID registeredBy;
	private UUID id;
	
	public String getName(){
		return this.name;
	}
	public void setName(String name){
		this.name = name;
	}
	public String getLogin(){
		return this.login;
	}
	public void setLogin(String login){
		this.login = login;
	}
	public UUID getRegisteredBy(){
		return this.registeredBy;
	}
	public void setRegisteredBy(UUID registeredBy){
		this.registeredBy = registeredBy;
	}
	public UUID getId(){
		return this.id;
	}
	public void setId(UUID id){
		this.id = id;
	}
}
```

## Using as command line executable

```bash
my@comp:~/code/schemas$ sudo npm install mongoose2pojo -g
my@comp:~/code/schemas$ mongoose2pojo image-schema.js
```

File `image-schema.js`.
```JS
var Schema = require("mongoose").Schema;

module.exports = new Schema({
  ref:  { type: Schema.ObjectId, ref: 'Asset', index: true },
  time: { type: Date, index: true },
  type: String
},
{
  collection: 'image'
});
```

File `ImagePojo.java` gets created:
```java
public class Image{
	private UUID ref;
	private Date time;
	private String type;
	private UUID id;
	
	public UUID getRef(){
		return this.ref;
	}
	public void setRef(UUID ref){
		this.ref = ref;
	}
	public Date getTime(){
		return this.time;
	}
	public void setTime(Date time){
		this.time = time;
	}
	public String getType(){
		return this.type;
	}
	public void setType(String type){
		this.type = type;
	}
	public UUID getId(){
		return this.id;
	}
	public void setId(UUID id){
		this.id = id;
	}
}
```
