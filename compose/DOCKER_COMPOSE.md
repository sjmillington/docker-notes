## Docker compose

2 components:
  - `YAML` file which describes the solution, volumes, networks, images etc..
  - CLI tool `docker-compose`

## Docker compose file

It has it's own version. `1, 2, 2.1, 3, 3.1 etc..`. This is the first line in the file.

Can be used with `docker-compose` or in production with `Swarm`

`docker-compose -f` we can change the `docker-compose.yml` file name to anything. such as `docker-compose-dev.yml`

**Not designed to be a production-grade tool**. But helps with local development.

### Commands

`docker-compose up` - starts
`docker-compose down` - stops, also removes all cont/volumes/networks
  - `-v` deletes all volumes used.

## Build

Will build Dockerfiles if not in the cache

Use 

```
build: .
image: custom-nginx
```

Or 

```
build:
  context: .
  dockerfile: something.Dockerfile
image: custom-nginx
```

This will look for `custom-nginx` and run the build if it's not in the cache.

We can trigger the build again with `docker-compose up --build` if it **is** in the cache








