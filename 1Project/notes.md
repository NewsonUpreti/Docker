# Running this test app. 

## structure of the app
| Files on duty |
| ------------- |
| Server.js |
| Html and css|



| Requirements |
| ------------- |
| Mongo|
| Mongo express (interface for the database) |




## Networking concepts used. 
* We want the above mongo and mongodb container to interact with each other.
* we create a separate network for them and put both the containers in that same network. 


## high level
* setting up mongo and mongo-express.
-d # we want detach mode.
-p27017:27017 # we want default port to communicate to mongo port.
--name #mongo-container
--network mongo-network #btw


* ENV setup
-e MONGO_INITDB_ROOT_USERNAME=admin MONGO_INITDB_ROOT_PASSWORD=qwerty


### mongo setup

```bash
 docker run -d \
-p27017:27017 \
--name mongo \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=qwerty \
--network mongo-network \
mongo
```



### mongo express setup
```bash
 docker run -d \
-p8081:8081 \
--name mongo-express \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=qwerty \
--network mongo-network \
-e ME_CONFIG_MONGODB_URL="mongodb://admin:qwerty@mongo:27017" \
∙ mongo-express
```

Now we can access localhost:8081 to access the gui of mongodb database. 
or we can run the server.js to get, post, etc.. to this server in this app. The server.js is local but database is running in a docker container.


### easy setting up the above database with docker compose with singleton yaml file
```yaml
services:
  mongo:
    image: mongo
    container_name: mongo
    ports:
      - "27017:27017"  # host:container port binding
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: qwerty

  mongo-express:
    image: mongo-express
    container_name: mongo-express
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADMINPASSWORD: qwerty
      ME_CONFIG_MONGODB_URL: mongodb://admin:qwerty@mongo:27017/
```
**Benefits of the above** 
* no need to explicitly create network, it automatically creates one for the serviced containers
