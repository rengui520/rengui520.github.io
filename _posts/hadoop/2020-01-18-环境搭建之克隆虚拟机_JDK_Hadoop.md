---
title:  环境搭建之克隆虚拟机_JDK_Hadoop
date:   2020-01-18 12:00:00
tag:    Hadoop
---

## 环境搭建之克隆虚拟机_JDK_Hadoop

利用 service + 服务名称 + start/stop/restart 对服务进行 启动，停止和重启
首先重连网络，运行
`service network restart`

一、Hadoop 运行环境搭建  
一）虚拟机准备 
1.克隆虚拟机

2.修改克隆虚拟机的静态 IP 
`vim /etc/udev/rules.d/<接口>`
把 rules.d 下的文件删除

配置网络
`vim /etc/sysconfig/network-scripts/ifcfg-ens33`
删除或注释 HWADDR 和 UUID 两行内容，设置子网 IP ，后重启 `reboot`   

3.修改主机名称：
`hostnamectl` //查询
`vim /etc/hostname` //进去后修改
`NETWORKING=yes`
centos6   vim /etc/sysconfig/network   

(  `vim /etc/hosts`)//每台机子都要填写自己的和其他机子的信息
```
192.168.21.13 hadoop001
192.168.21.14 hadoop002
```

4.关闭防火墙    
CentOS 7.0 默认使用的是 firewall 作为防火墙   

查看防火墙状态   
firewall-cmd --state   

停止 firewall   
systemctl stop firewalld.service   

禁止 firewall 开机启动   
systemctl disable firewalld.service    

5.创建用户

6.配置用户具有 root 权限
`vim /etc/sudoers`
```
linjing   ALL=(ALL)     ALL  //添加该行到 root 下
```
凡是系统配置，非 root 用户操作时，需在命令前加 `sudo`      

二、安装软件    
查询是否安装 Java 软件：
`rpm -qa | grep java`
如果安装的版本低于1.7，卸载该 JDK：
`sudo rpm -e 软件包`
查看 JDK 安装路径：
`which java`

1.下载
命令：`wget -P /保存文件的目录 文件下载地址`

2.安装
2.1 创建安装目录
```
cd /opt  
sudo mkdir module   //存放解析后的 Java、Hadoop 包
sudo mkdir software    //存放 Java、Hadoop 压缩包
sudo chown linjing:linjing module/ software/  //修改所在者、组
sudo chown linjing:linjing module/ software/ -R  //递归改变   
```
2.2 解压至安装目录
`tar -zxvf xxx.tar.gz -C /opt/module`   

4.设置环境变量
4.1 打开文件
`sudo vim /etc/profile`

4.2 在末尾添加
JDK 安装：  
```
##JAVA_HOME
export JAVA_HOME=/opt/module/jdk-13.0.2
export PATH=$PATH:$JAVA_HOME/bin
```

Hadoop 安装：
```
##HADOOP_HOME
export HADOOP_HOME=/opt/module/hadoop-3.2.1
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin
```

4.3 使环境变量生效
`source /etc/profile`

4.4 添加软链接
```
ln -s xxx  xxx
ln -s /opt/module/jdk-13.0.2/bin/java /usr/bin/java
```

4.5 检查
`java -version`

三、Hadoop 重要目录   
（1）bin 目录：存放对 Hadoop 相关服务（HDFS,YARN）进行操作的脚本
（2）etc 目录：Hadoop 的配置文件目录，存放 Hadoop 的配置文件
（3）lib 目录：存放 Hadoop 的本地库（对数据进行压缩解压缩功能）
（4）sbin 目录：存放启动或停止 Hadoop 相关服务的脚本
（5）share 目录：存放 Hadoop 的依赖 jar 包、文档、和官方案例
