---
title: 下载和上传文件
draft: true
---
```bash
scp /home/work/source.txt work@192.168.0.10:/home/work/   #把本地的source.txt文件拷贝到192.168.0.10机器上的/home/work目录下

scp work@192.168.0.10:/home/work/source.txt /home/work/   #把192.168.0.10机器上的source.txt文件拷贝到本地的/home/work目录下

scp work@192.168.0.10:/home/work/source.txt work@192.168.0.11:/home/work/   #把192.168.0.10机器上的source.txt文件拷贝到192.168.0.11机器的/home/work目录下

scp -r /home/work/sourcedir work@192.168.0.10:/home/work/   #拷贝文件夹，加-r参数
```


```bash
#!/bin/bash
 
printf "%-10s %-8s %-4s\n" name sex age
printf "%-10s %-8s %-4.2f\n" zhangsan man 32
printf "%-10s %-8s %-4.2f\n" lisi man 25
printf "%-10s %-8s %-4.2f\n" wangmeili woman 23
```

`%s` 字符串 
`%c` `%d` `%f` 都是格式替代符

`%-10s` 指一个宽度为10个字符（`-` 表示左对齐，没有则表示右对齐），任何字符都会被显示在10个字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来。

`%-4.2f` 指格式化为小数，其中 `.2` 指保留 2 位小数。



```bash
#!/bin/sh
 
echo ">>>>>>>>>"
echo -e "hello world! \c" # -e 开启转义 \c 不换行
echo ">>>>>>>>>"
 
echo `date`               # ``而非'',打印命令执行的结果
echo "............."
echo "输入姓名:"           #read读取前台输入信息
read name
echo "$name is my friend"
```