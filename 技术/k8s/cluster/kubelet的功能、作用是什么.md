### 1、节点管理

kubelet启动时会向api-server进行注册，然后会定时的向api-server汇报本节点信息状态，资源使用状态等，这样master就能够知道node节点的资源剩余，节点是否失联等等相关的信息了。master知道了整个集群所有节点的资源情况，这对于 pod 的调度和正常运行至关重要。

### 2、pod管理

kubelet负责维护node节点上pod的生命周期，当kubelet监听到master的下发到自己节点的任务时，比如要创建、更新、删除一个pod，kubelet 就会通过CRI（容器运行时接口）插件来调用不同的容器运行时来创建、更新、删除容器；常见的容器运行时有docker、containerd、rkt等等这些容器运行时，我们最熟悉的就是docker了，但在新版本的k8s已经弃用docker了，k8s1.24版本中已经使用containerd作为容器运行时了。

### 3、容器健康检查

pod中可以定义启动探针、存活探针、就绪探针等3种，我们最常用的就是存活探针、就绪探针，kubelet 会定期调用容器中的探针来检测容器是否存活，是否就绪，如果是存活探针，则会根据探测结果对检查失败的容器进行相应的重启策略；

### 4、Metrics Server资源监控

在node节点上部署Metrics Server用于监控node节点、pod的CPU、内存、文件系统、网络使用等资源使用情况，而kubelet则通过Metrics Server获取所在节点及容器的上的数据。

### 补充：

kubelet 是负责容器真正运行的核心组件，主要的职责如下所示：

- 负责 Node 节点上 Pod 的创建、修改、监控、删除等全生命周期的管理
- 定时上报本地 Node 的状态信息给 API Server
- kubelet 是 Master 和 Node 之间的桥梁，接收 API Server 分配给它的任务并执行
- kubelet 通过 API Server 间接与 Etcd 集群交互来读取集群配置信息
- kubelet 在 Node 上做的主要工作具体如下：
    1. 设置容器的环境变量、给容器绑定 Volume、给容器绑定 Port、根据指定的 Pod 运行一个单一容器、给指定的 Pod 创建 Network 容器
    2. 同步 Pod 的状态
    3. 在容器中运行命令、杀死容器、删除 Pod 的所有容器