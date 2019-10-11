## Scaling Out

## Overlay Multi-Host Networking

Swarm-wide bridge network drivers where containers can communicate across nodes.

- `--driver overlay` when creating network
- This is for container-to-container traffic **inside** a swarm.
- Each service can be connected to multiple networks 
  - E.g front-end back-end

`docker network create --driver overlay mydrupal`

#### Creating a Service Attached to the Overlay Network

For the back-end

`docker service create --name psql --network mydrupal -e POSTGRES_PASSWORD=mypass postgres:9.6`

`docker service create --name drupal --network mydrupal -p 80:80 drupal`

We can watch for it to be up: `watch docker service ls`

`docker service ps drupal`

And we can now access drupal by visiting any one of the nodes IP address - even though drupal will only be running on one node.

## Routing Mesh

- Automatically routes incoming packets for a service to a proper task.
- Spans all nodes in the swarm
- Uses IPVS from Linux Kernel
- Load balances swarm services across their tasks
- Two ways this works: 
  - Container-to-container in an overlay network (uses VIP)
  - External traffic incoming to published ports (all nodes listen)
  - We don't care which server the container is on. 

**notes**

- This is a stateless load balancing out of the box.
- This is layer 3 load balancer (TCP), not layer 4 (DNS).
- These can both be solved by using `nginx` or `HAProxy` to sit in-front.


