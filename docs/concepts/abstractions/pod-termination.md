---
---
<!--
#### <a name="pod-termination"></a> Pod Termination

Since Pods represent processes running on your cluster, Kubernetes provides for *graceful termination* when Pods are no longer needed. Kubernetes implements graceful termination by applying a default *grace period* of 30 seconds from the time that you issue a termination request. A typical Pod termination in Kubernetes involves the following steps:
-->
### <a name="pod-termination"></a> Pod 终止
因为Pods 其实是运行在集群上的进程，Kubernetes 为不再需要的 Pods 提供了一种*优雅终止*的方式， 当用户提出一个终止的请求时 Kubernetes 会设置一个默认 30 秒的 *grace period* 以达到优雅终止。 Kubernetes 里典型的 Pod 终止过程如下：

<!--
1. You send a command or API call to terminate the Pod.
1. Kubernetes updates the Pod status to reflect the time after which the Pod is to be considered "dead" (the time of the termination request plus the grace period).
1. Kubernetes marks the Pod state as "Terminating" and stops sending traffic to the Pod.
1. Kubernetes send a `TERM` signal to the Pod, indicating that the Pod should shut down.
1. When the grace period expires, Kubernetes issues a `SIGKILL` to any processes still running in the Pod.
1. Kubernetes removes the Pod from the API server on the Kubernetes Master.

> **Note:** The grace period is configurable; you can set your own grace period when interacting with the cluster to request termination, such as using the `kubectl delete` command. See the [Terminating a Pod]() tutorial for more information.
-->
1. 用户发起一个命令或者调用一个 API 去终止 Pod.
2. Kubernetes 更新 Pod 的状态来反映在 Pod 被认定成 "dead" 之后的时间。（终止请求的时间外加上 grace period).
3. Kubernetes 将 Pod 的状态标识成 "Terminating" 同时停止给 Pod 发送流量。
4. Kubernetes 给 Pod 发送一个 `TERM` 信号，表示要停止这个 Pod 。
5. 当 grace period 过期 Kubernetes 将向所有 Pod 里还在运行的进程发起 `SIGKILL`。
6. Kubernetes 将从 Kubernetes Master 的 API server 里移除 Pod。

>**注意：** grace period 是可以配置的， 用户可以在向集群提交终止请求时设置自己的 grace period, 比如说用 kubectl delete` 命令。详细内容参见 [Terminating a Pod]() 指南。
