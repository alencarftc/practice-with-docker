# Create the services network

### Create an overlay network named "internal"
docker network create -d overlay internal

### List all docker networks
docker network ls


# Create the services
### Create a MySQL service
docker service create --name mysql --network=internal --replicas 1 -e MYSQL_ROOT_PASSWORD=senha -e MYSQL_DATABASE=wordpress mysql

### Create a WordPress service connecting to the MySQL container
docker service create --name wordpress --network=internal --replicas 1 -p 80:80 -e WORDPRESS_DB_HOST=mysql:3306 -e WORDPRESS_DB_PASSWORD=senha -e WORDPRESS_DB_USER=root wordpress

# List all running services
docker service ls


References:
https://www.youtube.com/watch?v=Vu9lfasgPaM