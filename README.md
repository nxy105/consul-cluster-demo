# Consul Cluster Demo

There is a 6 node example consul environment running in Vagrant.

We are building:

- 2 consul servers
- 2 service nodes
- 1 consul agent hosting web gui
- 1 demo web app

```
$ git clone https://github.com/nxy105/consul-cluster-demo.git
$ cd consul-cluster-demo
$ vagrant up
```

### Notes

- Each node is wired to use 256mb ram, so this cluster should run OK on most systems.