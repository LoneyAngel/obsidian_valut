# 字节码文件
## 组成
### 部分

java文件字节码文件的组成 ![](https://cdn.nlark.com/yuque/0/2024/png/43222940/1731745129583-2e54f32d-2d14-4d74-8f8e-bd8b085333ad.png)
#### magic部分
![](https://cdn.nlark.com/yuque/0/2024/png/43222940/1731745185446-cefdf479-cf6a-45ac-a742-fd0d720349a7.png)
#### 版本号

![](https://cdn.nlark.com/yuque/0/2024/png/43222940/1731745109383-7ca31599-7576-4c8e-9459-97872598c40b.png)
#### 常量池
![](https://cdn.nlark.com/yuque/0/2024/png/43222940/1731745437196-67f5c1e2-a6bc-4eeb-a2eb-717f6fdb5203.png)

#### 方法
存放有字节码指令

##### 指令集：

| 指令      | 作用               |     |     |
| ------- | ---------------- | --- | --- |
| iconst  | 把值存到操作数栈中        |     |     |
| iload   | 把值从变量集合移到操作数栈中   |     |     |
| clinit  | 初始化类对象           |     |     |
| instore | 将操作数栈中的数存放到变量列表中 |     |     |
|         |                  |     |     |
|         |                  |     |     |
特殊的：
- **clinit
![[Pasted image 20241118133610.png]]


## 工具
### arthas介绍
	
	阿里的产品
	对运行时进行监控
#### 功能

![](https://cdn.nlark.com/yuque/0/2024/png/43222940/1731747790182-e0d97f36-d702-4315-af41-5c9efdc3973b.png)

监控面板：arthas-boot
##### 命令
-java -jar arthas的jar包
-dump 类的名字  返回已加载的类的字节码文件到指定的目录
-jad 类的名字 反编译已加载的类的源码


#### 应用场景
![](https://cdn.nlark.com/yuque/0/2024/png/43222940/1731753881028-c59d1754-3180-4fc9-ab98-defc5f83ca4e.png)





#### arthas-client
`arthas-boot.jar` 和 `arthas-client.jar` 是 Alibaba Arthas 工具的两个不同部分，它们各自有不同的功能和用途。下面详细解释它们之间的关系和各自的用途：

##### 1. `arthas-boot.jar`

`arthas-boot.jar` 是 Arthas 的启动器，用于启动 Arthas 并连接到目标 JVM 进程。它的主要功能包括：

- **启动 Arthas**：通过命令行启动 Arthas，并选择要连接的目标 JVM 进程。
- **端口管理**：允许你指定 Telnet 和 HTTP 服务的端口，避免端口冲突。
- **自动下载**：如果本地没有 Arthas 的相关文件，`arthas-boot.jar` 会自动下载所需的文件。

###### 使用示例

```
java -jar arthas-boot.jar
```

启动后，`arthas-boot.jar` 会列出当前系统中所有可用的 Java 进程，让你选择要连接的目标进程。你还可以通过命令行参数指定端口：

```
java -jar arthas-boot.jar --telnet-port 9998 --http-port -1
```

##### 2. `arthas-client.jar`

`arthas-client.jar` 是 Arthas 的客户端，用于连接已经启动的 Arthas 实例。它的主要功能包括：

- **连接 Arthas 实例**：通过 Telnet 或 HTTP 协议连接到已经启动的 Arthas 实例。
- **发送命令**：在连接到 Arthas 实例后，可以在客户端中输入和执行 Arthas 命令，进行各种调试和诊断操作。

###### 使用示例

假设你已经通过 `arthas-boot.jar` 启动了 Arthas，并且 Telnet 服务运行在端口 9998 上，你可以使用 `arthas-client.jar` 连接到这个实例：

```
java -jar arthas-client.jar 127.0.0.1 9998
```

##### 关系总结

- **启动与连接**：`arthas-boot.jar` 负责启动 Arthas 并连接到目标 JVM 进程，而 `arthas-client.jar` 负责连接

### javap

适合在服务器上查看指定的字节码文件的内容
因为并不是每个人都可以直接对服务器进行直接的操作

#### 步骤:
	如果jar包需要，先使用jar-xvf命令进行解压
	javap -v 字节码文件名称 （> 指定解析结果的存放位置）
	java -jar命令的使用场景

### jclasslib

	即平常使用比较方便
	有软件和插件
今后可能会经常使用





# 类的生命周期

## 加载

### 加载步骤

1. 类加载器根据类的全限定名通过不同的渠道以二进制流的方式获取字节码信息
2. 将字节码信息保存到方法区（方法区不是真实存在的）
3. ![[Pasted image 20241118113707.png]]
4. ![[Pasted image 20241118113717.png]]![[Pasted image 20241118113810.png]]
### 为什么需要在堆区复制一份
- 因为方法区中的部分是c++写的，java调用起来不太方便
- 堆中的部分去除了部分程序员用不上的部分
![[Pasted image 20241118114204.png]]


### 查看内存中的对象（可视化）
![[Pasted image 20241118114347.png]]
-cp指定jar包中的启动类
#### jps
java的cmd命令，查看所有java进程的类
  格式： 
进程号：   对应的类名
## 连接
### 验证
![[Pasted image 20241118115928.png]]
![[Pasted image 20241118120049.png]]
#### 版本号的检测
![[Pasted image 20241118120625.png]]


### 准备
- 为static静态变量分配内存并设置初值
-  final修饰，会直接赋值
![[Pasted image 20241118120749.png]]

### 解析
![[Pasted image 20241118121342.png]]


## 初始化阶段

执行静态代码块中的代码，并为静态变量赋值
![[Pasted image 20241118131909.png]]
### 触发类初始化的几种情况
![[Pasted image 20241118132139.png]]
### 应用场景
![[Pasted image 20241118134308.png]]
![[Pasted image 20241118134343.png]]![[Pasted image 20241118134430.png]]

# 类加载器