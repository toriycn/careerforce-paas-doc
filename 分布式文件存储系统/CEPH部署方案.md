# CEPH部署方案

##一、安装前准备
###1.1安装环境介绍

下载地址：http://download.ceph.com/tarballs/

不管你是想为云平台提供Ceph 对象存储和/或 Ceph 块设备，还是想部署一个 Ceph 文件系统或者把 Ceph 作为他用，所有 Ceph 存储集群的部署都始于部署一个个 Ceph 节点、网络和 Ceph 存储集群。 Ceph 存储集群至少需要一个 Ceph Monitor 和两个 OSD 守护进程。而运行 Ceph 文件系统客户端时，则必须要有元数据服务器（ Metadata Server ）。

![](media/14987030377996/14987040466654.png)

Ceph OSDs: Ceph OSD 守护进程（ Ceph OSD ）的功能是存储数据，处理数据的复制、恢复、回填、再均衡，并通过检查其他OSD 守护进程的心跳来向 Ceph Monitors 提供一些监控信息。当 Ceph 存储集群设定为有2个副本时，至少需要2个 OSD 守护进程，集群才能达到 active+clean 状态（ Ceph 默认有3个副本，但你可以调整副本数）。
Monitors: Ceph Monitor维护着展示集群状态的各种图表，包括监视器图、 OSD 图、归置组（ PG ）图、和 CRUSH 图。 Ceph 保存着发生在Monitors 、 OSD 和 PG上的每一次状态变更的历史信息（称为 epoch ）。
MDSs: Ceph 元数据服务器（ MDS ）为 Ceph 文件系统存储元数据（也就是说，Ceph 块设备和 Ceph 对象存储不使用MDS ）。元数据服务器使得 POSIX 文件系统的用户们，可以在不对 Ceph 存储集群造成负担的前提下，执行诸如 ls、find 等基本命令。

部署一套最简单的系统，需要3台机器。至少需要一个监控和两个osd。


ibm的文章：https://www.ibm.com/developerworks/cn/linux/l-ceph/
*我比较爱看，因为很多东西说的很明白。*


测试部署：
1）系统内核：2.6.32-358
![](media/14987030377996/14987065389614.jpg)

2)机器确认：
10.1.215.3/4/5

| IP | ROLES |HOSTNAME  |
| --- | --- | --- |
| 10.1.215.3 | ceph-deploy,Mon | 10.0.1.x 是public网络，10.0.2.x是cluster网络 |
| 10.1.215.4 | Osd |  |
| 10.1.215.5 | Osd |  |


写入测试：

| 测试内容 | 测试内容 |性能  |
| --- | --- | --- |
| 挂载方式大文件 |测试10个2G的文件  | 时间：  每机器占用的空间： |
| 挂载方式小文件 |测试10万个10K的文件  |时间：  每机器占用的空间：   |
| API方式大文件 |测试10个2G的文件  | 时间：  每机器占用的空间：  |
| API方式小文件 | 测试10万个10K的文件 | 时间：  每机器占用的空间：  |


http://www.vpsee.com/2015/07/install-ceph-on-centos-7/

![](media/14987030377996/14987089677398.png)


缺少部署的过程，后续再研究：
http://blog.csdn.net/yanghuichan/article/details/49303953

