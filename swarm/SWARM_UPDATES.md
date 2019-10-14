## Swarm Updates

Examples:

### Image

`docker service update --image myapp:1.2.1 <servicename>`

### Env Variables

`docker service update --env-add NODE_ENV=prod --publish-rm 8080`

`publish-rm 8088` - remove port
`publish-add 9090:80` - add port

### Num Replices 

`docker service scale web=8 db=6`

### Rebalancing

`docker service update --force web`