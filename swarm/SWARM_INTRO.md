# Swarm Intro

Containers everywhere = new problems

- How do we automate container lifecycle ? 
- How can we easily scale out/in/up/down ? 
- How can we ensure containers restart when the fail ?
- How can we replace containers without downtime (blue/green deploy) ?
- How can we control/track where containers get started ?
- How can we crate cross-node virtual envs?
- How can we ensure only trusted servers run our containers? 

**Swarm mode**

It's a clustering solution build inside docker

Not enabled out of the box - it has to be enabled.

Built of `manager nodes`and `worker nodes`

`docker service` replaces `docker run` 

A single service can have multiple tasks - each task is a container.

The swarm manager node will decide *where* in the swarm those containers will be placed.

## Checking Status

`docker info` and look for `Swarm`. It'll say `active` or `inactive`

## Activating

`docker swarm init`

- PKI and security automation
  - Root signing certificate create for the swarm
  - Certificate issued for the first manager
  - Join tokens are created

- Raft DB created to store root CA, configs and secrets
  - Encrypted on disk
  - No need to another key/value system to hold secrets
  - Replicates logs amongst managers via mutual TLS in 'control plane'

## Creating a Service

viewing: `docker node ls` - there will only be one Leader amongst Managers

`docker service create` creates orders.

`docker service create alpine ping 8.8.8.8` - returned ID is the service ID, and **not** the container ID

We can view current services with `docker service ls`

Can view the containers with `docker service ps <service ID>`

## Scaling up

`docker service update <service ID> --replicas 3`

If we remove a container with `docker container rm -f <id>`, swarm will spin up a new container.

## Shutting down

`docker service rm <service>`. 

This will also clean up the service tasks (containers) after some time

## Creating 3 Node Swarm

Need 3 linux OS for this.

Options:

- play-with-docker.com
  - Only needs a browser, but resets after 4 hours.
- docker-machine + VirtualBox
- digital ocean + docker install
  - Most like production setup, but codes $5/node/month
- Lots of other ways, AWS, Azure, Google cloud etc...

When using multiple machines, need to advertise the address

`docker swarm init --advertise-addr <IP>`

Copy + paste the swarm-join command on the other machines. This is printed to the terminal when the swarm is initialised

`docker swarm join --token <token> <IP>:<Port>`

They will join as workers.

`docker node ls` should now show 3 nodes

Workers will not be able to run swarm commands.

#### To Promote The Worker

`docker node update --role manager <node>`

#### Getting access to join tokens

`docker swarm join-token manager`

or 

`docker swarm join-token worker`

If a node is already in the swarm, we need to run `docker swarm leave` before the new `docker swarm join`