---
layout: post
title: Nginx代理Tomcat负载问题
categories: 系统运维
description: Nginx代理Tomcat负载问题。
keywords: 中间件,nginx，Tomcat

---

> 在SpringBoot项目中使用Oauth2做认证的时候，使用Nginx代理应用服务造成JWT不可用，本文记录其解决过程。

1、OAuth2 客户端应用采用的是HTTPS部署，而OAUTH2服务端使用HTTP部署，通过前置NGINX做了一层返向代理转发至服务端。

NGINX

```java
   proxy_set_header HOST $host;
   proxy_set_header X-Real-IP $remote_addr;
   proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
   proxy_set_header X-Forwarded-Proto https;
```

Tomcat

```java
<Engine >
    <Valve className="org.apache.catalina.valves.RemoteIpValve"  
    remoteIpHeader="X-Forwarded-For"  
    protocolHeader="X-Forwarded-Proto"  
    protocolHeaderHttpsValue="https"/> 
</Engine >
```

2.使用下划线的KEY存放JWT，导致使用NGINX转发后无法获取。

```java
headers.set("access_token", jwt);
```

在设置HEADER时，KEY使用了下划线，需要开启NGINX支持下划线

```shell
underscores_in_headers on;
```

3、Nginx负载问题

为了解决session共享问题，会使用ip_hash作为负载均衡算法。我们的客户端请求，首先是请求到一个网关服务，由网关服务再转发到Nginx，此时Nginx拿到的ip都是网关服务的，这样的话IP就会转发到一个节点，负责不均衡。可以通过自定义Hash策略来实现。

```
#获取用户真实IP，并赋值给变量$clientRealIP
map $http_x_forwarded_for $clientRealIp {
“” $remote_addr;
~^(?P<firstAddr>[0-9\.]+),?.*$ $firstAddr;
}
#通过自定义策略到相应的节点
upstream h5 {
hash $clientRealIp;
server 192.168.100.104:9080;
server 192.168.100.105:9080;
}
```

