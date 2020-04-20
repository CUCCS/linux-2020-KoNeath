# 实验三 #
### 动手实战Systemd ###
***
## 实验环境 ##
* **Ubuntu 18.04.4-server**
* **Asciinema recorder**
***
## Systemd：命令篇 ##
* **[systemd系统管理](https://asciinema.org/a/322021)**
* **[Unit]( https://asciinema.org/a/322029)**
* **[systemd 配置文件](https://asciinema.org/a/322031)**
* **[Target]( https://asciinema.org/a/322034)**
* **[日志管理](https://asciinema.org/a/322036)**
***
## Systemd：实战篇 ##
* **[实战](https://asciinema.org/a/322044)**
***
## 自查清单 ##
* 如何添加一个用户并使其具备sudo执行程序的权限？
```
sudo adduser username #添加一个用户
sudo usermod -a -G sudo username</pre> #将其加入sudo组中
```
* 如何将一个用户添加到一个用户组？
```
sudo usermod -a -G usergroup username
```
* 如何查看当前系统的分区表和文件系统详细信息？
```
sudo fdisk -l #查看分区表

df -a #查看文件系统详情
```
* 如何实现开机自动挂载Virtualbox的共享目录分区？
```
mkdir /mnt/share #虚拟机中创建共享目录

mount-t vboxsf share_file_name /mnt/share #挂载

share_file_name /mnt/share vboxsf default 0 0 #进入/etc/fstab进行编辑
```
* 基于LVM（逻辑分卷管理）的分区如何实现动态扩容和缩减容量？
```

sudo apt install lvm2 #安装lvm2包

sudo su #切换至root用户

lvdisplay #查看逻辑卷

lvextend --size +<大小>m <逻辑卷> #动态扩容

lvreduce --size -<大小>m <逻辑卷></pre> #缩减容量
```
* 如何通过systemd设置实现在网络连通时运行一个指定脚本，在网络断开时运行另一个脚本？
  * 编辑其配置文件的`service`区块：
    * `ExecStartPost=网络连通时运行的指定脚本`
    * `ExecStopPost=网络断开时运行脚本`
* 如何通过systemd设置实现一个脚本在任何情况下被杀死之后会立即重新启动？实现杀不死？
    * 编辑其配置文件的`service`区块：`Restart`字段修改为`always`
***
## 参考文献 ##
#### [Systemd 入门教程：命令篇 by 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)
#### [Systemd 入门教程：实战篇 by 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-part-two.html)