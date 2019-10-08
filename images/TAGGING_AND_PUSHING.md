# Tagging and Pushing to Docker Hub

default tag:

`<user>/<repo>:<tag>`

i.e `docker pull mysql/mysql-server:latest`

To tag a new image:

`docker image tag <image> <new-image>`

i.e 

`docker image tag nginx myrepo/nginx:my-cool-tag`

## To push

Auth 

`docker login` or `docker logout`

`docker image push <image>`

Existing layers won't be uploaded for new tags!
