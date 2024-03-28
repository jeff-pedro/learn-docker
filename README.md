# Learning Docker
> Used to explore the Docker world!

## Resources
- [Docker official doc]()

## Explored

### [Dockerfile]()

1. start app build with Dockerfile
```shell
docker run -dp 3000:3000 \ 
-w /app -v "$(pwd):/app" \
--network todo-app \
-e MYSQL_HOST=mysql \
-e MYSQL_USER=root \
-e MYSQL_PASSWORD=secret \
-e MYSQL_DB=todos \
node:18-alpine \
sh -c "yarn install && yarn run dev"
``` 

2. start database
```shell
docker run -d \            
--network todo-app --network-alias mysql \
-v todo-mysql-data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=secret \
-e MYSQL_DATABASE=todos \
mysql:8.0
```
 
### [Docker Compose]()
-
 
### Docker Swarm
- ...

