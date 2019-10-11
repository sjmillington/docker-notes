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

## Secrets

Secrets storage is built in.

Encypted on disk and in transit

A secret is any sensitive information
  - usernames & passwords
  - TLS certificates and keys
  - SSH keys
  - etc..

These are stored in the Swarm Raft DB

Only stored on the dik of the Manager nodes

Secrets are first stored in swarm (`docker secret`) then assigned to service.

Not all services can get access to all the secrets.

They look like a file in the container to th app, but are actually in-mem fs. 
 - `/run/secrets/<secret_name>`
 - key is the file name, value is the content.

Secrets are a swarm only thing. Local **docker-compose can use file-based secrets, but it's not secure**

To create the secret:

`docker secret create <secret_name> <file_with_secret>`





