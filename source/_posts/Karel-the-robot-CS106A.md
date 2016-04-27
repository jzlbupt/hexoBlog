title: Karel the robot CS106A
date: 2016-04-19
tags: [Karel,java,jdk]
categories: [技术,编程方法学]
---
不得不说，为了让小Karel出现在我的电脑屏幕上，我花了大半天的时间找原因，解决各种问题的过程让我对eclipse和jdk的设置有了更深刻的认识...
<!--more-->
___
## 问题list

###  Problem1: Failed to load the JNI shared library: "...\client\jvm.dll"
**原因**：安装的eclipse和jdk的32/64版本不一致，即如果eclipse是32位的，jdk必须也是32位的，相反如果是64位的eclipse，则必须是64位的eclipse

![d](/eclipse和jdk的位数不同.png)

###  Problem2: 跑起来小Karel之后，只显示空白窗口
**原因**：下载的assignment比较古老的原因，只能支持JDK6

###  Problem3: java.lang.UnsupportedClassVersionError: CheckerboardKarel : Unsupported major.minor version 52.0

描述：显示不支持的类加载器
**原因**：由于上一个问题，根据网上提供的一些解决方案，将程序的build path中的jre版本改为了1.6
![problem2-2](/problem2-2.png)
然后满心欢喜的运行小Karel程序，发现报错如下...
![问题2-2](/Karel-the-robot-CS106A/problem2-1.png)
![问题2-3](/Karel-the-robot-CS106A/problem2-3.png)
这是由于eclipse的jdk版本要求和程序不符，导致的错误。通过修改`Window`->
`Prefernces`->`Java`->`Compiler`->`Compiler compliance level`也为相同的1.6即可
![问题2-4](/Karel-the-robot-CS106A/Problem2-4.png)

### Problem 4: java -version 和 javac -version 的版本不一致

由于原安装的JDK版本是1.8，改为1.6之后就将环境变量`JAVA_HOME`修改为相应的路径，然后`cmd`看了一下`java -version`和`javac -version`，惊奇的发现java的版本还是1.8，而 javac的版本却已经是1.6了。在这里需要看一下环境变量中的`path`，如果有其他的环境变量也指向较高版本的jdk，那么就会覆盖掉后面设置的路径，将`%JAVA_HOME%\jre\bin`提到前面即可解决这个问题

## 哈~看下跑出来的小Karel
![Karel](/Karel-the-robot-CS106A/Karel.png)

