# jdk8线上程序oom定位与设置
## 首先启动程序设置发生oom生成dump文件

```java
-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=./java_heapdump.hprof

指定开启与设置dump日志存储位置
```

## 模拟oom代码

```java
    public static void main(String[] args) throws Exception {
        int     port            = 8888;
        int     ioThreads       = 4;           // I/O线程数
        int     businessThreads = 8;     // 业务线程数
        boolean      useNettyPool = true; // 使用Netty线程池
        List<byte[]> list         = new ArrayList<>();
        int          counter      = 0;

        while (true) {
            // 每次分配1MB的内存
            byte[] array = new byte[1024 * 1024]; // 1MB
            list.add(array);
            counter++;

            System.out.println("已分配 " + counter + " MB");

        }
//        new SingleReactorMultiThreadServer(port, ioThreads, businessThreads, useNettyPool).start();
    }
```


## 启动执行发生oom，并且生成dump文件

<img width="140" height="25" alt="企业微信截图_17660413783500" src="https://github.com/user-attachments/assets/e014a9a4-25e3-47f6-a7af-595d6ce8a62a" />

## 启动jvisualvm工具

<img width="793" height="139" alt="企业微信截图_17660413576913" src="https://github.com/user-attachments/assets/161ca58c-e95a-44df-9aea-2923715be152" />

<img width="910" height="475" alt="企业微信截图_17660413941669" src="https://github.com/user-attachments/assets/36c81c8e-1f43-4737-9f9d-99f194c01716" />

## 点击文件选择装入，就可以看到系列日志，同时工具也可以远程连接进行日志排查
<img width="240" height="155" alt="企业微信截图_17660414159052" src="https://github.com/user-attachments/assets/25a4ea1e-115a-4ea0-8fff-b23b05ff631e" />


<img width="477" height="408" alt="企业微信截图_17660414668880" src="https://github.com/user-attachments/assets/96ba8c4a-237f-4ea2-abe9-adf90c1a5611" />


<img width="580" height="641" alt="企业微信截图_17660414851369" src="https://github.com/user-attachments/assets/7fc92995-68ee-401a-bb5a-cbadf11daefc" />


