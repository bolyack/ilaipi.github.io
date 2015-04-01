---
layout: post
title: 上证报项目技术总结
category: 工作
keywords: scp nohup ProcessBuilder memory limit cpu
---

# 上证报项目技术总结

---

## Linux

### 1. scp命令
```
从一台Linux传输文件到另一台Linux。
用法：scp file1 file2 file3 uname@host:destFile
如果传输的包括文件夹，scp -r file1 file2 file3 uname@host:destFile
示例：
scp -r algo-fnode.jar lib/ fnode@172.20.10.62:/home/fnode/app
把当前目录下的algo-fnode.jar文件和lib文件夹传输到62的/home/fnode/app目录下
```

### 2. nohup

```
本地Linux调用远程Linux命令时，前面加上nohup，
可以在当前terminal关闭时远程Linux上的进程不关闭。
```

### 3. &

```
在终端中执行命令时，最后加上&，可以把命令转为后台进程
示例：nohup java -jar algo-fnode.jar &
```

## Java

### 1. 获取本机IP

```
    //已在windows/Linux测试过。
    //当使用vpn时获取到的ip有问题。
    public static String getLocalIp() {
        Enumeration e = null;
        try {
            e = NetworkInterface.getNetworkInterfaces();
        } catch (SocketException e1) {
            logger.warn("不能获取网络信息", e1);
            return null;
        }
        while (e.hasMoreElements()) {
            NetworkInterface n = (NetworkInterface) e.nextElement();
            Enumeration ee = n.getInetAddresses();
            while (ee.hasMoreElements()) {
                InetAddress i = (InetAddress) ee.nextElement();
                if (!i.isLoopbackAddress()) {
                    if (i instanceof Inet6Address) {
                        continue;
                    }
                    if (i instanceof Inet4Address) {
                        return i.getHostAddress();
                    }
                }
            }
        }
        return null;
    }
```

### 2. Java操作进程

```
        //通过java.lang.ProcessBuilder来创建Process。
        ProcessBuilder processBuilder = new ProcessBuilder();
        List<String> commoands = new ArrayList<>();
        commoands.add("java");
        commoands.add("-Xmx" + functionRuntime.getMemLimit() + "m");
        commoands.add("-XX:MaxPermSize=128M");
        commoands.add("-jar");
        commoands.add("algo-fnode.jar");
        commoands.add(args[0]);
        commoands.add(args[1]);
        processBuilder.command(commoands);
```

最好通过这种方式来设置command。也可以：
ProcessBuilder builder = new ProcessBuilder("java", "-jar"...);
但是不能：
ProcessBuilder builder = new ProcessBuilder("java -jar...");
这样会认为"java -jar..."是一个命令，而不会认为 -jar 是参数。

然后，

```
    Process process = processBuilder.start();
    //监听标准输出
    public String listenMsg() {
        InputStream inputStream = process.getInputStream();
        StringBuffer buffer = new StringBuffer();
        InputStreamReader reader = new InputStreamReader(inputStream);
        BufferedReader bufferedReader = new BufferedReader(reader);
        while (true) {
            try {
                String line = bufferedReader.readLine();
                if (line == null) {
                    break;
                }
                if (StringUtils.isBlank(line)) {
                    continue;
                }
                log(line);
                buffer.append(line).append(System.getProperty("line.separator"));
            } catch (IOException e) {
                logger.warn("监听进程输出时异常", e);
            }
        }
        return buffer.toString();
    }
```

### 3. Java控制进程占用内存资源

在运算节点中，需要通过独立进程调用对应的函数，可能是java函数，也可能是R函数。
针对不同的函数类型，有不同的内存控制方法。

#### 3.1 java函数

java函数就是通过java -jar命令启动一个进程，可以直接通过此命令的命令行参数：
```-Xmx xxxM```
设置最大堆占用内存

#### 3.2 R函数

R函数就是通过```Rscript xxx.R```命令启动一个进程，为了限制内存，需要在调用```Rscript```命令前
通过linux的```ulimt```命令进行限制。
而进程创建的时候只能指定一个命令，所以要把```ulimt```和```Rscript```命令封装到同一个sh脚本中。
然后调用sh脚本执行R函数。

### 4. Java控制进程占用CPU资源

可以通过```cpulimit```命令，通过进程```pid```设置进程的CPU占用率,
e.g. ```cpulimit -p 1122 -l 38```

### 5. Java获取系统空闲内存

通过执行linux命令：```free -m```，解析其输出，可得当前系统的空闲内存