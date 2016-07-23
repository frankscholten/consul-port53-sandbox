# Consul port 53 sandbox

## Goal

Run Consul on port 53 in Docker using it's own network interface. This currently does not work yet. See https://github.com/hashicorp/docker-consul/pull/24

## How to use

It uses the hashicorp/consul image with `EXPOSE 53/udp` added.

```
$ docker build -t hashicorp/consul .
$ docker run -v $PWD/config:/opt/config --cap-add NET_BIND_SERVICE hashicorp/consul agent -config-dir=/opt/config
==> Starting Consul agent...
==> Starting Consul agent RPC...
==> Consul agent running!
         Node name: '682cf0e620be'
        Datacenter: 'dc1'
            Server: false (bootstrap: false)
       Client Addr: 127.0.0.1 (HTTP: 8500, HTTPS: -1, DNS: 53, RPC: 8400)
      Cluster Addr: 172.17.0.2 (LAN: 8301, WAN: 8302)
    Gossip encrypt: false, RPC-TLS: false, TLS-Incoming: false
             Atlas: <disabled>

==> Log data will now stream in as it occurs:

    2016/07/23 14:49:35 [INFO] serf: EventMemberJoin: 682cf0e620be 172.17.0.2
    2016/07/23 14:49:35 [ERR] agent: failed to sync remote state: No known Consul servers
```

In a different terminal connect to port 53 on the container

```
$ dig @172.17.0.2
<blocks>
```

## Get in touch

If you know how to fix this please comment on the above PR thread or via Twitter at @frank_scholten
