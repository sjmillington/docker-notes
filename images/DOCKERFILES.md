# Dockerfiles 

### Common Keywords

Each keyword will create a new layer in the image.

- `FROM` - base image
- `ENV` - environment variables
- `RUN` - run in the shell at build time. It's a good idea to group together lots of shell commands together to reduce the layers.
- `EXPOSE` - export the ports. -p on the host is still needed on `docker run`.
- `CMD` - command run when the container is launched. Only one is allowed per `Dockerfile`
- `WORKDIR` - basically cd. Best practice to use this when changing directory.
- `COPY` - copy `from` `to`


### Building the image

`docker image build -t repo:tag .`

When the image is built a second time, cached steps will be skipped.

**keep things that are changed a lot at the bottom of the file**