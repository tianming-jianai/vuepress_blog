# Idea 使用指南

[Getting started | IntelliJ IDEA (jetbrains.com)](https://www.jetbrains.com/help/idea/getting-started.html)

## idea 激活

[教程](http://blog.idejihuo.com/topics/jetbrains) [激活码](http://jets.idejihuo.com/)

## 创建代码片段

1. 位置：File->Settings->Editor->Live Templates    添加Live template
2. 简称、描述、代码片段、试用范围
3. 代码片段
4. 光标：$START$、$END$ 
5. 变量

**示例**

```java
// test 测试方法
/**
* 
*/
@Test
public void test$START$(){
    $END$
}

// logs 日志输出转字符串
log.info(String.valueOf($END$));
```

## 隐藏不想看到的文件

Setting -> Editor -> File Types -> Ignore File and Folders

输入要隐藏的文件名，支持*号通配符

## 快速编码

### 快速foreach一个可迭代集合

`iter`：自动生成最近代码块中的可迭代对象的foreach迭代方式
