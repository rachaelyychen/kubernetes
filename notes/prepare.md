## 前期准备

1.参考资料

<a href="http://hutao.tech/k8s-source-code-analysis/" target="">k8s源码分析(release-1.13)</a>

<a href="https://blog.tianfeiyu.com/source-code-reading-notes/" target="">k8s源码阅读(release-1.16)</a>

<a href="https://github.com/mcsos/understanding-kubernetes" target="">k8s源代码解析</a>

<a href="https://item.jd.com/12665791.html" target="">Kubernetes源码剖析</a>

2.配置环境

```
[root@node4 ~]# cat /etc/redhat-release
CentOS Linux release 7.3.1611 (Core) 
[root@node4 ~]# uname -r
3.10.0-514.el7.x86_64
[root@node4 ~]# go version
go version go1.16.2 linux/amd64
```

3.搭建集群

使用 kubeadm 搭建单节点集群用于调试源码，过程略。
```
[root@node4 ~]# kubeadm version
kubeadm version: &version.Info{Major:"1", Minor:"14", GitVersion:"v1.14.3", GitCommit:"5e53fd6bc17c0dec8434817e69b04a25d8ae0ff0", GitTreeState:"clean", BuildDate:"2019-06-06T01:41:54Z", GoVersion:"go1.12.5", Compiler:"gc", Platform:"linux/amd64"}
[root@node4 ~]# kubectl get po -n kube-system -o wide
NAME                            READY   STATUS    RESTARTS   AGE   IP             NODE    NOMINATED NODE   READINESS GATES
calico-node-g4plp               2/2     Running   10         29m   10.154.2.204   node4   <none>           <none>
calico-typha-5677469c75-s7sxp   1/1     Running   6          29m   10.154.2.204   node4   <none>           <none>
coredns-8686dcc4fd-mdl5n        1/1     Running   0          31m   172.16.0.3     node4   <none>           <none>
coredns-8686dcc4fd-mq7z8        1/1     Running   0          31m   172.16.0.2     node4   <none>           <none>
etcd-node4                      1/1     Running   0          30m   10.154.2.204   node4   <none>           <none>
kube-apiserver-node4            1/1     Running   0          30m   10.154.2.204   node4   <none>           <none>
kube-controller-manager-node4   1/1     Running   0          30m   10.154.2.204   node4   <none>           <none>
kube-proxy-2f2n9                1/1     Running   0          31m   10.154.2.204   node4   <none>           <none>
kube-scheduler-node4            1/1     Running   0          30m   10.154.2.204   node4   <none>           <none>
```

4.准备源码

使用 GoLand 远程部署项目至服务器，过程略。
```
[root@node4 kubernetes]# ls
api    BUILD.bazel        CHANGELOG.md  cmd                 CONTRIBUTING.md  Godeps  LICENSE  Makefile                  notes   OWNERS_ALIASES  plugin     SECURITY_CONTACTS  SUPPORT.md  third_party   vendor
build  CHANGELOG-1.14.md  cluster       code-of-conduct.md  docs             hack    logo     Makefile.generated_files  OWNERS  pkg             README.md  staging            test        translations  WORKSPACE
```

编译 scheduler 组件。
```
[root@node4 kubernetes]# cd cmd/kube-scheduler/
[root@node4 kube-scheduler]# ls
app  BUILD  OWNERS  scheduler.go
[root@node4 kube-scheduler]# go build .
[root@node4 kube-scheduler]# ls
app  BUILD  kube-scheduler  OWNERS  scheduler.go
```











