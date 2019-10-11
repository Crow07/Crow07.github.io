---
title: helm简介
date: 2019-10-11 14:27:00 +0800
categories: [Blogging, Tutorial]
tags: [kubenetes]
seo:
  date_modified: 2019-10-11 14:27:41 +0800
---
我们可以将Helm看作Kubernetes下的apt-get/yum。Helm是Deis (https://deis.com/) 开发的一个用于kubernetes的包管理器。每个包称为一个Chart，一个Chart是一个目录（一般情况下会将目录进行打包压缩，形成name-version.tgz格式的单一文件，方便传输和存储）。

对于应用发布者而言，可以通过Helm打包应用，管理应用依赖关系，管理应用版本并发布应用到软件仓库。

对于使用者而言，使用Helm后不用需要了解Kubernetes的Yaml语法并编写应用部署文件，可以通过Helm下载并在kubernetes上安装需要的应用。

除此以外，Helm还提供了kubernetes上的软件部署，删除，升级，回滚应用的强大功能。
##helm
***

####安装实践
1.kubeasz部署的kubenetes集群在/etc/ansible/bin下面有helm的二进制文件，可以直接拿来使用
2.部署tiller的时候helm init可能会失败，换阿里的源即可：

```
helm init --upgrade -i registry.cn-hangzhou.aliyuncs.com/google_containers/tiller:v2.9.1 --stable-repo-url https://kubernetes.oss-cn-hangzhou.aliyuncs.com/charts
```

3.遇到错误

```
failed to list: configmaps is forbidden: User“system:serviceaccount:kube-system:default” cannot list configmaps in the namespace “kube-system”
```

执行以下命令创建 serviceaccount tiller 并且给它集群管理权限:

```
kubectl create serviceaccount --namespace kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'
```

参考文档：
[helm简介安装配置使用指南](https://blog.csdn.net/bbwangj/article/details/81087911)
[https://helm.sh/docs/](https://helm.sh/docs/)
[https://whmzsu.github.io/helm-doc-zh-cn/quickstart/quickstart-zh_cn.html](https://whmzsu.github.io/helm-doc-zh-cn/quickstart/quickstart-zh_cn.html)
[https://blog.csdn.net/qq_35959573/article/details/80885052](https://blog.csdn.net/qq_35959573/article/details/80885052)