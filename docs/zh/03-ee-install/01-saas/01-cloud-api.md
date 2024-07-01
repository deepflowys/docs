---
title: 对接公有云 API
permalink: /ee-install/saas/cloud
---

# 简介

DeepFlow 平台对所有观测数据自动化注入`云资源`、`K8s 资源`和`K8s 自定义 Label`标签，这些标签是 DeepFlow 可观测性分析的基础，因此 DeepFlow 在开始工作之前需首先完成云、容器集群各类资源信息的学习。

DeepFlow 通过 云平台的 API 接口自动对接学习公有云租户的资源标签，通过 K8s 集群的 apiserver 自动对接学习容器资源标签。

# 创建云平台（阿里公有云）

- 创建步骤
1. 进入「资源」-「资源池」-「云平台」
2. 点击“新建云平台”
3. 填写“云平台”相关信息，点击“确定”，得到云平台

| 配置项 | 填写内容 | 备注 |
|-------|-----|--------|
| 云平台名称 | 例：aliyun-1	| 云平台的名称，可自定义 |
| AccessKey ID	 | 例：LTAI4FiU3ad3txLUSRg8xGfn	 | 请在阿里云控制台-accesskeys 页面上配置用于 API 访问的密钥 ID（只读权限即可） |
| AccessKey Secret	 | 例：itsHzkPo22jbtNZ61QEz3gc5bsPnXP	 | 请在阿里云控制台-accesskeys 页面上配置用于 API 访问的密钥 KEY（只读权限即可） |
| 区域白名单	 | 例：华南3（广州）, 华北6（乌兰察布）	 | 可以配置多个，不支持正则表达式；优先级高于区域黑名单；具体取值可参考阿里云 ECS 地域和可用区列表 |

- API 说明

DeepFlow 会使用如下 API 从阿里公有云对接学习资源信息，如果需要限制 DeepFlow 能够学习的资源项，可在阿里云控制台限制 AK/SK 的权限：

| API | 对接内容 | 是否必须项 |
|-------|-----|--------|
| DescribeRegions |    |     | 
| DescribeVpcs |    |     | 
| DescribeNatGateways |    |     | 
| DescribeSnatTableEntries |    |     | 
| DescribeForwardTableEntries |    |     | 
| DescribeRouteTableList |    |     | 
| DescribeRouteEntryList |    |     | 
| DescribeVSwitches |    |     | 
| DescribeInstances |    |     | 
| DescribeNetworkInterfaces |    |     | 
| DescribeSecurityGroups |    |     | 
| DescribeSecurityGroupAttribute |    |     | 
| DescribeLoadBalancers |    |     | 
| DescribeLoadBalancerAttribute |    |     | 
| DescribeHealthStatus |    |     | 

# 创建容器集群

DeepFlow 观测覆盖的 K8s 集群分类两类：
1. 附属容器集群——指容器集群的 Node 使用的是 DeepFlow 在某个云平台中学习到的云服务器；
2. 独立容器集群——指容器集群的 Node 与 DeepFlow 在某个云平台中学习到的云服务器没有关联；

> 注：如果部署 K8s 集群的云服务器已经通过云平台对接自动学习到某个云平台，那么该 K8s 集群必须要对接或录入为该云平台的附属容器集群，否则将导致 DeepFlow 的可观测性数据打标时无法确定数据所属的云平台，从而产生数据标签的紊乱。

因此，在 DeepFlow 中创建容器集群分为三种场景：
- 创建云平台后，自动创建附属容器集群
- 创建云平台后，手动创建附属容器集群
- 创建独立容器集群

## 自动创建附属容器集群

对部分公有云 K8s 产品，DeepFlow 能够通过公有云 API 自动学习 K8s 集群信息，并在「资源」-「资源池」-「云平台」中自动创建附属容器集群，无需运维人员操作。

已支持的公有云产品包括：
- 阿里ACK

## 手动创建附属容器集群

对于公有云租户自建 K8s 集群，或通过公有云 API 无法自动学习的 K8s 集群，需要运维人员手动在 DeepFlow 的「资源」-「资源池」-「云平台」中手动录入附属容器集群。

**TBD：此处有待插入图片**

## 创建独立容器集群

独立容器集群的创建可以由 DeepFlow Server 在收到该 K8s 集群的首个 DeepFlow Agent 注册信息后自动在创建，无需运维人员操作。


# 检查

检查云平台对接状态：

**TBD：此处有待插入图片**