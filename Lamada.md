## lambda表达式

### 1.1 lambda表达式的一般语法

```java
(Type1 param1, Type2 param2, ..., TypeN paramN) -> {
  statment1;
  statment2;
  //.............
  return statmentM;
}
```
### 1.2 单参数语法
当lambda表达式的参数个数只有一个，可以省略小括号

```java
param1->{
  statment1;
  statment2;
  //.............
  return statmentM;
}
```
### 1.3 单语句写法

当lambda表达式只包含一条语句时，可以省略大括号、return和语句结尾的分号


```java
param1 -> statment
```


### 1.4 方法引用写法

（方法引用和lambda一样是Java8新语言特性，后面会讲到）

```java
Class or instance :: method
```
