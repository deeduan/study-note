## jMeter 压测

### 安装jMeter(mac)

#### java环境依赖

jMeter依赖java环境, 所以我们先要检查安装java环境:

```bash
java --version
```

运行以上命令检测系统是否已经安装了java命令, 如果已经安装, 跳过安装java环境步骤。

jMeter依赖java8+ 我们这里安装java8, 当然你也可以根据jMeter的要求安装合适的java环境,[java8下载传送门](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
安装完成之后检查java和java_home

```bash
java --version
/usr/libexec/java_home -V
```
以上命令运行结果响应正确则表示已经安装成功。接下来我们配置环境变量(类unix环境, win请自行百度)

```bash
vim ~/.bash_profile #打开profile文件
```

在文件末尾添加如下内容:

```
export JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_221.jdk/Contents/Home"
export PATH="$JAVA_HOME/bin:$PATH:."
export CLASSPATH=".:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar"
```
其中JAVA_HOME内容由`/usr/libexec/java_home -V`可得到。

####jMeter安装

环境依赖问题解决后, 马上安装本尊jMeter [传送门](http://jmeter.apache.org/download_jmeter.cgi), 笔者安装的是 `Binaries apache-jmeter-5.1.1.tgz`。下载apache-jmeter-5.1.1.tgz,解压缩进入到对应目录,运行`ls`然后`cd`进入到bin目录, 运行如下命令即可启动jMeter,尽情享受测试带来的乐趣(改bug)吧.

```bash
sh jmeter
```
