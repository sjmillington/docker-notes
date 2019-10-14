## Full App Lifecycle

Local `docker-compose up` for dev
Remote `docker-compose up` for CI
Remote `docker stack deploy` to deploy production

### Pushing files together

We want to overlay 2 files to easily specify which image to use.

The `docker-compose.yml` file only concerns the images. We can also have a `prod` file or a `test` file with specific mounts and secrets. 

Specifying 2 files in the `docker-compose -f ` will push them together to create different staged files.

Config will print the combined file config to the screen, `>` will make it.

i.e:

To view: `docker-compose -f docker-compose.yml -f docker-compose.prod.yml config`

To create: `docker-compose -f docker-compose.yml -f docker-compose.prod.yml config > production.yml`


