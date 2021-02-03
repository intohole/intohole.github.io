---
layout: post
title: JAVA 好的包裹收集
tags: [tech]
city: 南京
---


背景
---------
JAVA & 算法日常开发，站在巨人的肩膀，最大化自己效率，把自己的精力，用在核心地方（重复造轮子，精力过于分散;功能迭代需要大量失败），为此收集日常使用中见到的好的包


+ fastjson
   - alibaba出品
   - ```java
     JSONObject json = JSONObject.parseObject("{\"name\":\"hello world!\"}");
     System.out.println(json);
     ```
+ lettuce
   - [官方网址](https://lettuce.io/)
   - [github](https://github.com/lettuce-io/lettuce-core)
   - 高级Redis客户端，用于线程安全同步,异步和响应使用,支持集群,Sentinel,管道和编码器。
   - 可以用redis cluster方式实现mget,且性能绝佳(主要考虑耗时问题)
   - [Redis高级客户端Lettuce详解](https://www.cnblogs.com/throwable/p/11601538.html)
   - ```java
      @Test
      public void testSetGet() throws Exception {
         RedisURI redisUri = RedisURI.builder()                    // <1> 创建单机连接的连接信息
            .withHost("localhost")
            .withPort(6379)
            .withTimeout(Duration.of(10, ChronoUnit.SECONDS))
            .build();
      RedisClient redisClient = RedisClient.create(redisUri);   // <2> 创建客户端
      StatefulRedisConnection<String, String> connection = redisClient.connect();     // <3> 创建线程安全的连接
      RedisCommands<String, String> redisCommands = connection.sync();                // <4> 创建同步命令
      SetArgs setArgs = SetArgs.Builder.nx().ex(5);
      String result = redisCommands.set("name", "throwable", setArgs);
      Assertions.assertThat(result).isEqualToIgnoringCase("OK");
      result = redisCommands.get("name");
      Assertions.assertThat(result).isEqualTo("throwable");
      // ... 其他操作
      connection.close();   // <5> 关闭连接
      redisClient.shutdown();  // <6> 关闭客户端
   }
  ```
