---
title: kubenetes-deploy-kubeasz
date: 2019-10-11 14:27:00 +0800
categories: [Blogging, Tutorial]
tags: [kubenetes]
seo:
  date_modified: 2019-10-11 17:26:08 +0800
---

kubeasz项目致力于提供快速部署高可用k8s集群的工具, 同时也努力成为k8s实践、使用的参考书；基于二进制方式部署和利用ansible-playbook实现自动化；既提供一键安装脚本, 也可以根据安装指南分步执行安装各个组件。

## 安装指南
***
### 项目地址

[https://github.com/easzlab/kubeasz](https://github.com/easzlab/kubeasz)



本次实验环境使用allinone的方式部署
```本次实验环境使用allinone的方式部署
# 下载工具脚本easzup，举例使用kubeasz版本2.0.2
export release=2.0.2
curl -C- -fLO --retry 3 https://github.com/easzlab/kubeasz/releases/download/${release}/easzup
chmod +x ./easzup
# 使用工具脚本下载
./easzup -D
./easzup -S
```