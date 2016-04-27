title: java环境配置
date: 2016-04-10
tags: java
categories: 技术
---
本文简要介绍java环境变量的配置，每次都忘一些细节，也给自己做个备份
<!--more-->
## Download jdk [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
## execute jdk-8u77-windows-x64.exe
- see more info [here](http://docs.oracle.com/javase/8/docs/)

## 配置环境变量

1. GOTO Computer -> Properties -> Advanced system settings -> Environment Variables
2. Set System variables
- **JAVA_HOME**: C:\Program Files\Java\jdk1.8.0_77
- **Path**: %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
- **Classpath**: .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar
- **tips**: JAVA_HOME变量配置时末尾没有“；”
Classpath配置时前面记得要有“.;"
最好配置系统变量

## some tips for ItelliJ IDEA
- `Ctrl+N`
- `Ctrl+N+Space`
- `Alt+Enter` for possible problem