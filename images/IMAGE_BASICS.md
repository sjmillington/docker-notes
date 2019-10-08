# Image Basics

- The application binaries and dependencies for the app + metadata of how to run it.
- Not a complete OS. 
  - The host provides the kernel
- Can be as small as one file (Like in GO)

Docker hub contains a load of official and non-official images.

Images a versioned with tags `image:tag`.

Official images are looked after by Docker themselves.

**Best practice** - specify the EXACT version, 1.11.9 for example NOT latest.

## Layers

Images are built with the union file system concept.

Layers can be seen with the history command:

`docker history nginx`

Each layer gets a unique sha:

```
---IMAGE
[ sha 4] [install curl]
[ sha 3] [change env variable]
[ sha 2] [update apt]
[ sha 1] [ubuntu]
----

```

Another image which also uses ubuntu, would use the ubuntu layer.

The layers are stored in the image cache.

```
---IMAGE 1   ----IMAGE 2
[   sha4    ][    sha7   ]
[   sha3    ][    sha6   ]
[   sha2    ][    sha5   ]
[          sha1          ]
----

```

Containers just create a new R/W layer on top of the base image. 

### Copy On Write (Cow)

When containers modify a file from the base image, the file is copied into the container layer.

### <Missing>

Not actually missing, it's just the layers aren't images themsevles, so no ID is assigned.





