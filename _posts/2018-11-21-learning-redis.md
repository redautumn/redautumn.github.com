---
title: "Learning redis"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post redis'
comments: true
date: 2018-11-21 11:10:41 EST
---

Just use this article to collect some common lessons/issues around redis.

## Received `(error) MOVED ` when trying to set values to redis in `redis-cli`

When you try to set a key/value pair in redis-cli, and received the following error:
```
root@redis-2-6cddfb8f96-n8cd5:/data# redis-cli
127.0.0.1:6379> set mykey test
(error) MOVED 14687 10.3.0.220:6379
```

As documented in redis document - [Moved redirection](https://redis.io/topics/cluster-spec#moved-redirection), it means the request has been redirected to a different node, and you should use `redis-cli -c` option to follow the redirect.

> A Redis client is free to send queries to every node in the cluster, including slave nodes. The node will analyze the query, and if it is acceptable (that is, only a single key is mentioned in the query, or the multiple keys mentioned are all to the same hash slot) it will lookup what node is responsible for the hash slot where the key or keys belong.

If the hash slot is served by the node, the query is simply processed, otherwise the node will check its internal hash slot to node map, and will reply to the client with a MOVED error, like in the following example:

GET x
-MOVED 3999 127.0.0.1:6381

```bash
$ redis-cli -c
```


## Find out the cluster node information

The CLUSTER NODES command can be sent to any node in the cluster and provides the state of the cluster and the information for each node according to the local view the queried node has of the cluster.

```bash
$ redis-cli cluster nodes
```

## Find out the version of redis cluster

Just be aware of the difference between `redis_version` and the redis gem file version. They don't map to each other one by one.

```bash
$ redis-cli info
```

## Flush redis cache

```bash
$ redis-cli> flushall
```

## Redis cluster - data sharding and fail-over

Redis doesn't use consistent hashing for data sharding as cassandra does. Instead, it uses a fixed hash-slot (16384, 0 - 16383) for data distribution. Basically every node in a cluster will be responsible for a subset of the slots. And to determine which slot a key belongs to, basically we can use CRC16 of the key modulo 16384.
And redis use master/slave to support high availability and fail-over. For each master node, it has at least one slave node, and when the master node is down, the slave node can continue working.

- [Redis cluster tutorial](https://redis.io/topics/cluster-tutorial)
- [Deep dive into Redis Clustering](https://medium.com/@pubuduboteju95/deep-dive-into-redis-clustering-1d71484578a9)
