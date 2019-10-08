# Docker Networking

Port check

`docker container port <container>`

## Default Networks

- Containers connected to a private virtual network 'bridge'
- Each VN routes through NAT firewall on host IP
- All containers on a network can talk without -p
- Best practice:
  - New virtual network for each app.

To find the network:

`docker container inspect --format '{{.NetworkSettings.IPAddress}} <container>`

#### Commands 

`network..`

`ls` - list
`inspect` - inspect
`create --driver` - create network
`connect` - attach network to a container
`disconnect` - detach

#### Common networks

`bridge` is the default docker virtual network which is NAT'ed behind the Host IP

`host` gains performance by skipping virtual networks but sacrifices security

`none` not attached

#### New networks

Created with a bridge driver. This allows containers to communicate with each other when running on the same docker host.

`docker network create my_app_net`

#### Connecting

`docker container run -d --name new_nginx --network my_app_net nginx`

#### Inspecting

`docker network inspect my_app_net`

output: 

```
 ...
  "Containers": {
      "0ce3cc60e67381911ef244a0e31974f9816771610147ba9262df9f8103755c13": {
          "Name": "new_nginx",
          "EndpointID": "519bacf21a88a1d55861861b4dbd6aa759b7a37e51a847fa40fbe34b2db7c72d",
          "MacAddress": "02:42:ac:12:00:02",
          "IPv4Address": "172.18.0.2/16",
          "IPv6Address": ""
      }
  },

```

## DNS

Forget IPs. 

Statis IPs and using IPs for talking to containers is an anti-pattern. **AVOID IT!**

Docker daemon has a built-in DNS server that containers use by default

It uses container names as the DNS

E.g if we have 2 nginx containers running: `my_nginx` & `new_nginx`. we can run:

`docker container exec -it my_nginx ping new_nginx`

The bridge network does not have the DNS server built in - it's easier to create a new network for your apps.

