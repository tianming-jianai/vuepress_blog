# Java 

## Java 图书

- Java 世界 著名人物

| James Gosling : Java之父      |      |      |
| ----------------------------- | ---- | ---- |
| **Rod Johnson：Spring创始人** |      |      |
|                               |      |      |
|                               |      |      |

[Java十大杰出人物2008](https://blog.csdn.net/java2000_net/article/details/3479105)

- Java 经典图书 

| [Effective Java 第三版](https://www.bookstack.cn/books/effective-java-3rd-chinese) :book: |
| ------------------------------------------------------------ |
| Java并发编程实战 [并发编程之美](https://www.bookstack.cn/books/java-concurrency-note):book: |
| [写给大忙人的Java SE 核心技术](https://pan.baidu.com/)       |
| [写给大忙人的Java SE 8核心技术](https://pan.baidu.com/):book: |
| [写给大忙人的Java SE 9核心技术](https://pan.baidu.com/):book: |
|                                                              |
|                                                              |
|                                                              |
|                                                              |
|                                                              |
|                                                              |

- Java 在线文档

| [凤凰架构](https://icyfenix.cn/)                             |
| ------------------------------------------------------------ |
| [Java 笔记](https://www.bookstack.cn/books/sdky-java-note) :thumbsup: |
| [java 面试手册](https://www.bookstack.cn/books/java_interview_manual) |
| [设计模式 Java版本](https://www.bookstack.cn/books/design-pattern-java) |
|                                                              |
|                                                              |
|                                                              |
|                                                              |
|                                                              |
|                                                              |



## 卸载JDK8 安装JDK 17

- 卸载JDK8

```bash
# 查看安装了哪些jdk安装包
rpm -qa | grep jdk
# 逐个卸载安装包
rpm -e --nodeps java-1.8.0-openjdk-1.8.0.312.b07-2.el8_5.x86_64
rpm -e --nodeps java-1.8.0-openjdk-headless-1.8.0.312.b07-2.el8_5.x86_64
rpm -e --nodeps nodeps copy-jdk-configs-4.0-2.el8.noarch
# 测试jdk是否被卸载
java --version
```

- 安装JDK17

```bash
yum list java-17-openjdk
yum install -y java-17-oepnjdk
# 测试jdk是否被安装
java --version
```

> OpenJDK 缺少很多使用工具：jstack、jps

- 安装OracleJDK17

[下载](https://www.oracle.com/java/technologies/downloads/#java17) [官方指导](https://docs.oracle.com/en/java/javase/17/install/installation-jdk-linux-platforms.html)

```bash
# 下载RPM包，wget很慢，字节下载到本地，然后上传
wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.rpm
scp .\jdk-17_linux-x64_bin.rpm root@ip:/java/package
```

Upgrade the required package using the following command:

```
$ rpm -Uvh jdk-17.interim.update.patch_linux-x64_bin.rpm
```

Delete the `.rpm` file if you want to save disk space.

Exit the root shell.   It is not required to reboot.

In addition, users can check which specific RPM package provides the `java` files:

```
Copy$ rpm -q --whatprovides java
```

