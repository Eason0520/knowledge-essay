sda4

## 一.安装前知识及工具

### 1. ISO镜像文件

ISO是光盘的镜像文件，就是我们可以用ISO文件来刻录到光盘或者u盘中，进行安装系统。

```
ISO镜像官网（阿里云）:https://developer.aliyun.com/mirror/?spm=5176.10695662.1173276.1.52312a32O9lTs1
ISO镜像官网:https://mirrors.ustc.edu.cn/centos/7.9.2009/isos/x86_64/
ISO镜像官网（中国外国语大学镜像站）：https://mirrors.bfsu.edu.cn/centos/7.9.2009/isos/x86_64/
```

注意：记得下载完把.iso文件名改成Centos.iso，方便引导的时候引用。



## 二.安装Centos7

1.把U盘插到电脑上，设置开机U盘启动 ps：按F12或F2或F10可选择U盘，选择U盘后跳转到下图界面

![img](assets/Window安装Linux系统/1215316-20170808134807261-1327986157.png) 

2.按下键盘TAB键将最下面的vmlinuz initrd=initrd.img inst.stage2=hd:LABEL=CentOS\x207\x20x86_64 quiet 改为 **vmlinuz initrd=initrd.img linux dd quiet** 然后，按“F10”保存修改或ctrl+x进入到后续界面，然后就可以看到所有的盘了，找到LABEL中包含Cenots的磁盘，然后记住设备名称(我的是sda4)，执行reboot重启操作。

```
setparams 'Install CentOS Linux 7'
linuxefi /images/pxeboot/vmlinuz inst.stage2=hd:LABEL=CentOS\x207\x20x86_64 quiet
initrdefi /images/pxeboot/initrd.img
```

![在这里插入图片描述](assets/Window安装Linux系统/8cbafc0bf8414aa6a71af76782e7f42e.png)

3.重启后到第三步界面按下TAB键，将vmlinuz initrd=initrd.img inst.stage2=hd:LABEL=CentOS\x207\x20x86_64 rd.live.check quiet 改为 vmlinuz initrd=initrd.img inst.stage2=hd:/dev/**sda4** quiet  ps：sda4就是你看到的启动盘名称

4.之后等待安装到图形界面，选择中文→English→点击继续(continue)

![image-20240324140133337](assets/Window安装Linux系统/image-20240324140133337.png)

5.时间、键盘、语言、软件等选择，点击每一个图标即可进入某一项设置中；

set-timezone Asia/Shanghai （说明：在Linux系统中设置系统的时区为上海时区，北也就是中国标准时间（CST），通常称为北京时间（Beijing Time））



系统分盘：如果嫌麻烦就选择默认分区，分区之前把系统盘清空就行了（ 别把启动盘选中了）

如果手动分区看下面，自动分区略过；注意下图不要使用默认的LVM，而是改为Standard Partition，核对磁盘分区标准
磁盘分区为“Standard Partition”而非默认的LVM，此项非常重要，“Standard Partition”模式要比LVM模式快5倍左右：

!(assets/Window安装Linux系统/1215316-20170808141045183-1479677038.png)

![img](assets/Window安装Linux系统/a404b10f7642f88595ffa8d4053c0958.png)



![在这里插入图片描述](assets/Window安装Linux系统/e9b63b6e799e4631864542325b5968ed.png)

![在这里插入图片描述](assets/Window安装Linux系统/6a98f31a91c64acfaaadd7e5f529aed8.png)

如果是以UEFI方式启动，会有多个boot分区，这几个boot分区保持默认不变即可

![在这里插入图片描述](assets/Window安装Linux系统/17e1c163efb648af829a3226c04b5613.png)

![在这里插入图片描述](assets/Window安装Linux系统/cc8cfb402b6a4ac9868c3ee6375ed786.png)

下面这一步分区很重要：
对于有两块或更多硬盘的机器，选择/home，将/home改为/data，后点击modify按钮，弹出的选择磁盘窗口一定要只选择一块最大的硬盘（或者RAID盘），然后把/data目录挂载到这个最大的硬盘（或者RAID盘）。
如果服务器只有一块硬盘，就删除/home或者/data挂载点。
对于150G或更小的系统盘，swap设置为16G；对于更大的系统盘，swap设置为32G。
最后把根目录/调整到最大，初swap外其他分区格式均为xfs，根目录要挂载到系统盘上（一般为ssd）。

![在这里插入图片描述](assets/Window安装Linux系统/56a6d81e3d734163bdb795e19286fd23.png)

![在这里插入图片描述](assets/Window安装Linux系统/eb18ae6dc2a2446ea0f4f34a7354b718.png)

![在这里插入图片描述](assets/Window安装Linux系统/a203f8d24dcb43d58bced4d9fde1e067.png)

![在这里插入图片描述](assets/Window安装Linux系统/5dbc6de7c02447cfa81dd0682d155bc9.png)

![在这里插入图片描述](assets/Window安装Linux系统/667700f1a87e4570922ca0fd683c0b40.png)

![在这里插入图片描述](assets/Window安装Linux系统/4b8e772d6bb04a87a9bee495f744dd44.png)



6.设置密码，可以先不设置用户。设置的密码要记得哦::::: root  R00t123456   eason eason0210

![在这里插入图片描述](assets/Window安装Linux系统/7fbcb38440fe463e96157fb9b06ae129.png)

![在这里插入图片描述](assets/Window安装Linux系统/0315896154ba480fb9797619d7d82e39.png)

安装完成后重启

![在这里插入图片描述](assets/Window安装Linux系统/3af1d00418b44804b35205c0ea0efcb3.png)

![在这里插入图片描述](assets/Window安装Linux系统/ac7e651b69544c82b38b325c8ab7ffc4.png)

![在这里插入图片描述](assets/Window安装Linux系统/6749c94706b9426faee4b3c0e9b8afc0.png)



配置服务器
ifconfig不能用
使用 ip addr 查看网卡名称是： enp2s0
vi /etc/sysconfig/network-scripts/ifcfg-enp2s0 把 ONBOOT 改成 yes
重启网卡：service network restart
更新所有的repo: yum update
安装网络工具： yum -y install net-tools 才能使用 ifconfig 和 netstat 等
使用 ifconfig 找到了内网IP： 192.168.31.214
通过putty登录如下：（下图可以看到所有的硬盘都被使用了。哦耶）

![在这里插入图片描述](assets/Window安装Linux系统/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpaGVuZ3prag==,size_16,color_FFFFFF,t_70#pic_center.png)





![img](assets/Window安装Linux系统/v2-d04859ac083621843e734cbd7185732a_720w.webp)

****

重启网络，命令行：`service network restart`

*3.3.4 配置DNS* 修改NetworkManager.conf 配置文件

```text
vim /etc/NetworkManager/NetworkManager.conf
```

在[main]中添加 	

```text
dns=no
```

![img](assets/Window安装Linux系统/v2-dfb37861b5c039e70ade7dc9c993684b_720w.webp)

修改resolv.conf配置文件

```text
vim /etc/resolv.conf
```

添加

![img](assets/Window安装Linux系统/v2-2a8268b5bf1a51fedde1e67111b521f3_720w.webp)



```text
#主DNS服务器，虚拟机中一般dns1设置为网关，2设置为外网dns
nameserver 192.168.10.2

#备DNS服务器
nameserver 114.114.114.114
```

重启NetworkManager

```text
systemctl restart NetworkManager
```