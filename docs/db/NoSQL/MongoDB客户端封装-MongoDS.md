MongoDB客户端封装-MongoDS
===

## 介绍
针对MongoDB客户端封装。客户端需自行引入依赖。

## 使用

### 引入依赖

```xml
<dependency>
	<groupId>org.mongodb</groupId>
	<artifactId>mongo-java-driver</artifactId>
	<version>3.12.10</version>
</dependency>
```

### 配置

在ClassPath（或者src/main/resources）的config目录下下新建mongo.setting

```
#每个主机答应的连接数（每个主机的连接池大小），当连接池被用光时，会被阻塞住 ，默以为10 --int
connectionsPerHost=100
#线程队列数，它以connectionsPerHost值相乘的结果就是线程队列最大值。如果连接线程排满了队列就会抛出“Out of semaphores to get db”错误 --int
threadsAllowedToBlockForConnectionMultiplier=10
#被阻塞线程从连接池获取连接的最长等待时间（ms） --int
maxWaitTime = 120000
#在建立（打开）套接字连接时的超时时间（ms），默以为0（无穷） --int
connectTimeout=0
#套接字超时时间;该值会被传递给Socket.setSoTimeout(int)。默以为0（无穷） --int
socketTimeout=0
#是否打开长连接. defaults to false --boolean
socketKeepAlive=false

#---------------------------------- MongoDB实例连接
[master]
host = 127.0.0.1:27017

[slave]
host = 127.0.0.1:27018
#-----------------------------------------------------
```

### 使用

```java
//master slave 组成主从集群
MongoDatabase db = MongoFactory.getDS("master", "slave").getDb("test");
```

