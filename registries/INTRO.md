## Registries

- We need a registry to be part of the container plan. 

### Docker Hub

It is a registry, but also contains auto-building.

- Can set up web hooks

If using GitHub, **DONT** use the `+ Create Repository` button. Use `Create Automated Build` instead. This allows us to build images based on code commits pushed to GitHub. Accounts need to be linked first.

- Can link other repositories, so that when they get rebuilt, ours does too. This is good for when we depend on other images in a dockerfiel. 

### Docker Registry

Can be privately on the network. Docker/distribution is the current regsitry. It's on GitHub, written in Go.

Not as full featured as Hub or others, no web UI and only basic auth.

It's basically just a web API and storage system.

Storage supports local, S3 and lots more.

- Docker won't communicate with the registry unless it has HTTPS

`docker container run -d -p 5000:5000 --name registry registry`

We need to tag with the host as well, now.

`docker tag hello-world 127.0.0.1:5000/hello-world`

`docker push 127...hello-world` - this will now push to the local registry, and not Docker hub.

`docker pull 127.0..hello-world`

To persist the registry

`docker container run -d -p 5000:5000 --name registry -v $(pwd)/registry-data:/var/lib/registry registry`


- It also works in swarm. We can add the registry to a node.
- Because of the routing mesh, all nodes can see 127.0.0.1:5000

Can view the catalog. go to:

`endpoint/v2/_catalog`

Result: `{"repositories":["hello-world"]}`

- It's cool to set up your own.. But it's probably best to use a hosted one. 