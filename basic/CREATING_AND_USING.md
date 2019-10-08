# Creating and Using Docker Containers

## Checking the install and config

Deploy a simple docker container to ensure it's all working as expected.

`docker version` or `docker info`

If a permission denied message occurs. Run this and log out and back into your account:

`sudo usermod -a -G docker $USER`

Get a list of options:

`docker`

## Running commands

Run the management commands:

`docker <ManagementCommand> <Command>` i.e `docker container run`

## Images

Image is the binary and libraries and source code that make up the application

## Containers 

Running instance of the image

## Image Registries 

Places where images are stored, such as Docker Hub 

## Example

`docker container run --publish 80:80 nginx`

- Pulls down latest image from Docker Hub
- Starts a container published on port 80.
- Routes traffic to the container IP 80

`--detach` will run it in the background.

`--name <name>` will add a custom name

#### List containers

Running containers

`docker container ls`

All containers (even stopped ones)

`docker container ls -a`

#### Stop the container

`docker container stop <containerId>` (The ID only needs to be enough characters to be unique)


#### View the logs

`docker container logs <name>`

#### View processes in the continer

`docker container top <name>`

#### Remove 

`docker container rm [list of ids]`

If it is running, stop it first or add `-f` to force it.

#### Passing environment variables

`-e MY_ENV_VARIABLE=yes`

## What happens in the background

`docker container run --publish 80:80 image`

- looks for image locally, if not found, it'll look on Docker Hub & download it. `image:latest` is used by default.
- Creates a new container based on the image and prepares to start
- Gives it a virtual IP on a private network inside docker engine.
- Opens up port `80` on host + forwards to port `80` in container
- Starts the container by using the `CMD` in the image `Dockerfile`

## Docker is NOT a VM 

It's just a process, it runs all software on the host machine.

## Runing MySQL

MySQL has a `MYSQL_RANDOM_ROOT_PASSWORD=yes/no` env variable. The password can be found in the logs