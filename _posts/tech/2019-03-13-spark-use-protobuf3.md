---
layout: post
title: spark任务使用protobuf3.x
tags: [tech]
city: 上海 
---

背景
---------
+ spark依赖protobuf 是2.x,如果使用3.x版本会出现下列错误
```java
   NoClassMetodError:com.google.protobuf.*
```
+ 原因
    - spark优先加载自己的包，所以你用什么方法都会使用spark2.x方法
    
+ 解决方法（maven工程），使用plgin插件，将依赖的protobuf3.x包，进行路径重命名，这样保证整体工程在编译的时候避免直接使用spark
    ```java
        <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <filtering>false</filtering>
            </resource>
        </resources>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>1.4</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <artifactSet>
                                <includes>
                                    <include>*:silkroad*</include>
                                    <include>*:protobuf*</include>
                                </includes>
                            </artifactSet>
                            <shadedArtifactAttached>false</shadedArtifactAttached>
                            <relocations>
                                <relocation>
                                    <pattern>com.google.protobuf</pattern>
                                    <shadedPattern>shaded.com.google.protobuf</shadedPattern>
                                </relocation>
                            </relocations>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ```
