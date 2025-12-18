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

## 启动jvisualvm工具

## 点击文件选择装入，就可以看到系列日志，同时工具也可以远程连接进行日志排查

