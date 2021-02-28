IO流是什么IO流有哪些类别.md

### 什么是IO?
- IO就是Input/Ouput,指数据读取到内存,和数据从内存向外输出的过程

### IO流分为几种?

1. Java标准库的java.io包提供了同步IO功能：
- 字节流接口：InputStream/OutputStream； (二进制数据以byte为最小单位在InputStream/OutputStream中单向流动；)
- 字符流接口：Reader/Writer。(字符数据以char为最小单位在Reader/Writer中单向流动。)
> 上面我们讨论的InputStream、OutputStream、Reader和Writer都是同步IO的抽象类，对应的具体实现类，以文件为例，有FileInputStream、FileOutputStream、FileReader和FileWriter。
2. java.nio是异步IO。