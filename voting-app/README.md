# Concepts
- Auto load balancing
- Rolling updates
- Roll-back a task

### Create the vote service
docker service create \
--name vote \
--replicas 4 \
--publish 5000:80 \
instavote/vote

### Update the service image
docker service update \
--image instavote/vote:indent \
vote

### Update the rolling update config
docker service update \
--update-parallelism 2 \
--update-delay 10s \
vote

### Update the service image
docker service update \
--image instavote/vote:movies \
vote

### Rollback the service image
docker service rollback vote


-----------------------------------------


### Create a healthy service
docker service create --name whoami \
--replicas 2 \
--update-failure-action rollback \
--update-delay 10s \
--update-monitor 10s \
--publish 8000:8000 \
lucj/whoami:1.0

### Update service using a buggy image
docker service update \
--image lucj/whoami:2.0 \
whoami


References:
https://betterprogramming.pub/rollout-and-rollback-in-docker-swarm-7f19e2fe2cd1
