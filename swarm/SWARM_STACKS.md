# Stacks

Basically compose files for production swarm

`docker stack deploy -c compose_file.yml <stack_name>`

Manages services, networks and volumes. 

New `deploy:` key. `build:` is not allowed.

**Builds should not be done in production swarms - this should be the job of CI or something similar**

By default, `docker-compose` will ignore `deploy` & `Swarm` will ignore `build:`

`docker-compose` not needed on Swarm server - it's just a development tool.

## Stack files

compose files, but need to be at least `version: 3`.

`docker stack ls` shows current stacks

`docker stack ps <stack_name>` shows current tasks

`docker stack services <stack_name>` shows all services with replices

`docker stack rm <stack_name>` to remove it all

**important**

Once you move to using a stack file, stick to it. Don't start typing in commands manually. Treat the file as the **source of truth**






