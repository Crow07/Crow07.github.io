---
title: prometheus-operator-helm部署
date: 2019-10-11 14:27:00 +0800
categories: [Blogging, Tutorial]
tags: [kubenetes]
seo:
  date_modified: 2019-10-11 14:27:41 +0800
---

##

####部署

######helm获取prometheus-operator安装包
```
helm fetch stable/prometheus-operator
```

######创建prometheus-operator专属的命名空间
```
kubectl create ns monitoring
```

######一键安装prometheus-operator
可以指定参数启动例如：
--set prometheus.service.type=NodePort  
--set prometheus.service.nodePort=30090，也可以 -f 指定value.yaml文件启动
```
helm install -f values.yaml  .  --name prometheus-operator  --namespace monitoring
```

######卸载prometheus-operator
```
helm delete prometheus-operator --purge
```

######升级prometheus-operator
```
helm  upgrade prometheus-operator -f values.yaml  .
```

####遇到的问题
1.每次删除prometheus-operator之后需要清理自建的crd：
```
kubectl delete crd prometheuses.monitoring.coreos.com
kubectl delete crd prometheusrules.monitoring.coreos.com
kubectl delete crd servicemonitors.monitoring.coreos.com
kubectl delete crd podmonitors.monitoring.coreos.com
kubectl delete crd alertmanagers.monitoring.coreos.com
```
2.部署完发现ServiceMonitor 不能发现kube-controller-manage和etcd以及schedule,是因为组件启动的时候监听的是127.0.0.1,改为监听0.0.0.0即可

参考：
[https://www.servicemesher.com/blog/prometheus-operator-manual/](https://www.servicemesher.com/blog/prometheus-operator-manual/)

####alertmanager告警接收器receiver webhook


####helm安装包prometheus-operator目录学习