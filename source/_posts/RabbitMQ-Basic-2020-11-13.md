---
title: RabbitMQ Basic
date: 2020-11-13 16:15:22
tags:
- JavaScript
---

### 组成部分说明如下：
- Broker：消息队列服务进程，此进程包括两个部分：Exchange和Queue。
- Exchange：消息队列交换机，按一定的规则将消息路由转发到某个队列，对消息进行过虑。
- Queue：
- 消息队列，存储消息的队列，消息到达队列并转发给指定的消费方。
- Producer：消息生产者，即生产方客户端，生产方客户端将消息发送到MQ。
- Consumer：消息消费者，即消费方客户端，接收MQ转发的消息。

### 消息发布接收流程：
#### `1.发送消息`
1. 生产者和Broker建立TCP连接。
1. 生产者和Broker建立通道。
1. 生产者通过通道消息发送给Broker，由Exchange将消息进行转发。
1. Exchange将消息转发到指定的Queue（队列）
#### `2.接收消息`
1. 消费者和Broker建立TCP连接
1. 消费者和Broker建立通道
1. 消费者监听指定的Queue（队列）
1. 当有消息到达Queue时Broker默认将消息推送给消费者。
1. 消费者接收到消息。

#### 常用 SH 命令
``` Bash
# Listing exchanges
sudo rabbitmqctl list_exchanges
# In this list there will be some amq.* exchanges and the default (unnamed) exchange. 
# 一般不直接把消息发给 queue，即使发了，也有一个默认的exchange name = ""
```

``` Bash
# Listing bindings
rabbitmqctl list_bindings
```

#### exchange 的分类
``` js
// 绑定 交换机和队列
channel.bindQueue(queue_name, exchange_name, 'black');

```
- fanout：第三个参数(binding key)不起作用
- direct