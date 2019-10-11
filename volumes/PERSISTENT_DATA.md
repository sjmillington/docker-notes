# Persistent Data

Containers and usually immutable and ephemeral

We want to only deploy containers, not change them.

### What about Databases?

We shouldn't mix unique (persistent) data  with containers.

We should use `separaration of concerns`

Two ways to do this - `Volumes` and `Bind Mounts`

- `Volumes` - make a special location outside of the containers Unique File System (UFS). e.g. on the host
- `Bind Mount` - Link container path to host path.

## Data Volumes

`VOLUME` command in the Dockerfile.

Volumes need manual deletion - they don't go when the container is deleted.

Volumes can be found in the config `docker inspect image`
  - This is shown in the `Mounts` section.

All Volumes can be seen with `docker volume ls`

These can be created with `docker volume create`, but are usually done in docker files or at run time.

### Named volumes


Can specify the named volume with `-v name:/path/to/volume`

`docker container run -d --name mysql -v my-volume:/var/lib/mysql mysql`

Now we can inspect `docker volume inspect my-volume`

## Bind Mounts

Map of host file or directory to a container file or directory.
  - The two locations point to the same folder on disk

They can't be used in a dockerfile

Same as named volumes, but a path is specified instead of a name:

`..container run -v /Users/user/app:/container/path/app <image>`

To use the current directory

`-v $(pwd):/usr/share....`



