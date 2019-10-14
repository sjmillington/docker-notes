
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

#### To create the secret:

`docker secret create <secret_name> <file_with_secret>`

Will return an id for the secret.

Can also be done from the commandLine

`echo "myDBpassWORD!" | docker secret create psql_pass -`

This is not recommended - as it also goes into the log file for the root user.

#### To view

`docker secret ls`

`docker inspect <secret_name>` - this wont reveal the actual secret!

##### To use:

`docker service create --name psql --secret psql_pass --secret psql_user -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass -e POSTGRES_USER_FILE=/run/secrets/psql_user postgres`

#### To remove:

`docker service update --secret-rm`

If a secret is removed, the container will be redeployed. 

### Using Secrets in Swarm Stacks

Secrets are defined in the `secrets` section of a compose file.

```
services:
  ...
  psql:
    image: postgres
    secrets:
      - my_secret
    environment:
      POSTGRES_PASSWORD_FILE: /run/secrets/my_secret

  secrets:
    my_secret:
      file: ./secret_file.txt

```

Removing the stack will also remove the secrets.


### Secrets in Docker Compose

They work just the same as in swarms, no need to change anything. 

**These are not secure**. It's just a bind mount into the container.

It only works with file based secrets + not the `external` version


