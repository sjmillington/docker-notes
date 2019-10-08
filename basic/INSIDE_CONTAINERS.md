# Inside containers

## Process Monitoring

#### Current processes:

`docker container top <name>`

#### View setup config:

`docker container inspect <name>`

JSON array about how the container was started is returned.

#### View statistics

`docker container stats <name>`

Opens a list of current stats. Ctrl+C to quit.

`docker container stats` for all containers

## Getting inside 

No need for SSH

- `docker container run -it` - for new ones.
- `docker container exec -it` - run command in an existing container.

`t` is pseudo tty, `i` is interactive (session open);

e.g. 

`docker container run -it -name proxy nginx bash`

`exit` to exit.

- Re-starting a container and getting inside:

`docker container start -ai <name>`

`-a` is attach


#### Common way to get in

`docker container run -it <name> bash`