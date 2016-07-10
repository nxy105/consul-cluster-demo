# Consul Cluster Demo

该项目作为 [Consul 搭建服务框架（使用篇）](http://joshuais.me/consul-da-jian-fu-wu-kuang-jia-shi-yong-pian/) 讲解中使用的一个示例。

在本项目中，我们构建了:

- 2台 Consul 服务端节点。
- 2台业务服务节点。
- 1台状态查看节点。
- 1台 Web 服务提供节点。

```
$ git clone https://github.com/nxy105/consul-cluster-demo.git
$ cd consul-cluster-demo
$ vagrant up
```

### 注意

- 每个节点限制使用256M内存，以便在不同的环境中都能运行。