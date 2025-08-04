# Docker

## 1. What is docker? Why do we need it.

## 2. Docker Images and Containers.

### **Best Example** Consider Images similar to classes, and objects similar to containers.

### About Images:

- Id: Each images will be allocated with an ID.
- Tags: Simply the versions of our images. (Useful for different versions and variants of the same project basically.)

- **Creating containers** : With docker image we can start creating containers. **CMD:** `docker run IMAGE_NAME`
  - As long as we keep creating, the new instance of the containers OR New containers will be created.

## 3. Installation of Docker cli and desktop.

- go to [docker website](https://www.docker.com) and follow the instructions based on your computer OS and architecture.
- Recommended: Download lazydocker for cli centric docker usage.

## 4. Important Docker commands

- Pulling docker image :
```bash
docker pull IMAGE_NAME
```
- run image:
```bash
docker run IMAGE_NAME
```
- run in interactive mode:
```bash
docker run -it IMAGE_NAME
```
- run in interactive mode, remove on exit:
```bash
docker run --rm -it IMAGE_NAME # gives terminal access basically
```
- only pull the image to local:
```bash
docker pull
```
- pull image + create container + run:
```bash
docker run
```
- list all available containers:
```bash
docker ps -a
```
- list all active/running containers:
```bash
docker ps
```
- start docker containers:
```bash
docker start CONT_NAME or CONT_ID
```
- stop docker containers:
```bash
docker stop CONT_NAME or CONT_ID
```
- remove docker image:
```bash
docker rmi IMAGE_NAME
```
**NOTE: ** If there's existing container made with this image, we have to force delete, or stop and delete the containers to normally delete.
- remove container:
```bash
docker rm CONT_NAME
```

- run container in detach mode (default mode is attach mode) :
```bash
docker run -d IMAGE_NAME
```
- specify name while running/creating a container:
```bash
docker run --name CONT_NAME -d IMAGE_NAME
```
- bind host port to container port: **EG:** `
```bash
docker run -p 8080:3306 IMAGE_NAME
```
and whatever is necessary. **NOTE:** _Same ports can be used for containers but the host port but be one and only connected to a singleton container_

### Troubleshooting Commands.

```bash
docker logs CONT_ID
```

**Running commands on already running containers** - basically accessing the live terminal.

```bash
docker exec -it CONT_ID /bin/sh
```
  **Example: ** WE want a quick sql learning session, we can simply
```bash
docker pull mysql && docker run -d -e MYSQL_ROOT_PASSWORD=root --name mysqltest mysql && docker exec -it mysqltest /bin/sh
```

- **SILLY ERROR ** running images like ubuntu, without interactive mode instantly closes it, so always is seen as exited status.

### Pulling Images.

- If we don't use tags, eg. `docker pull mysql`, it'll use default tag as latest version. to target tag, we use something like `docker pull mysql:8.0`
- Even if we pull different versions of same image, some layers are same and logs as already exists if other version images exists with matching layers.

### Running Images.

- while running images like mysql, to set the root password, etc.. we declare the env variable with `-e` prefix

  - Example: To run a 8.0 version mysql: `docker run --name mysql8.0 -d -e MYSQL_ROOT_PASSWORD=secret mysql:tag` , recommended to refer [mysql dockerhub](https://hub.docker.com/_/mysql) for detailed commands and information. **NOTE:** _no need to use tag for latest_

-

## 5. Docker vs VM
### first we need to understand the levels of a machine
| Computer |
| ------------- |
| Application layer: All applications runs here|
| Host OS : Kernel|
| Hardware: Base |



 | Docker   | Virtual machine    |
 |--------------- | --------------- |
 | virtualization on the application layer | Virtualizes in the Application layer and Host OS / Kernel level.             |
 | Easy setting up and getting started   | comparatively harder setting up.    |
 | Less overhead: lighter and faster   | More overhead: Heavier and slower, but necessary in many cases.   |
 |highly aligned towards linux    | Platform independent as it runs on it's own kernel   |


 

## 6. Port Mapping & setting Env Variables

### port binding

- By default, All docker containers have port assigned to them. (independent from the host machine)
- We can bind the host port to the container port with `-p` flag. **EG:** `docker run -p 8080:3306 IMAGE_NAME`

## 7. Troubleshooting containers
> [!info] Refer commands



## 8. Developing with Docker: Using containers to build Node Application

## 9. Dockerization of Node.js Application (Dockerfile).

## 10. Docker compose
### a. Services.
### b. Port Mapping.
### c. Env Variables.
### d. Volumes.

## 11. Publising to DockerHub.

## 12. Layering in Docker Images.

| Layers in Docker Image                  |
| --------------------------------------- |
| container (top level: Writable layer)   |
| layer 2                                 |
| layer 1                                 |
| Base layer: (Linux: eg. alpine, debian) |

**NOTE: ** All the layers are readonly/immutable layers other than the container.

 in this way, if we are using same image of different versions: It'll log already exists while pulling the layers. **Best Example: ** _If mysql uses ubuntu v20, then mysql:8.0 may use ubuntu v20 too, hence it logs already exists if we have either of them already._

## 13. Volume Mounting.

## 14. Docker Networking.
### a. Default and Custom Networks.
### Using custom network for multi-container apps.
### Network drivers: Bridge, Host, Null.
