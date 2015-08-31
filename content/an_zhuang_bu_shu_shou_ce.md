#安装部署手册 

##镜像获取

澜云提供基于安全的公有镜像供用户使用，所有镜像经定制化技术改造，不同于以往，用户不需要专业的安装技术，满足简单易用的原则，用户可从澜云**官方**提供的**七牛云存储地址**下载镜像安装包，通过澜云提供的自动化安装脚本，用户只需几行简单命令，即可完成安装。  

## 安装说明
用户在下载镜像文件后,在安装之前，有几点需要说明，用户在自己的机器上指定一台可连接外网的机器作为master node,master node节点的机器作为整个机器集群的中枢，承担着连接内外网的媒介作用，需要为master节点的机器设置外网IP,minion节点机器支持离线功能。master节点对机器的硬件性能要求较高，要求承担master node的机器具备4核、8G内存和至少50g的硬盘空间。此外，若干台作为minion node。然后安装部署Docker及相应组件。安装镜像的情景主要有两种，用户可根据具体情景进行安装,主要情景有：
* 
**在一个新环境中开始部署**
* 
 **重新部署master节点**
##镜像安装文件
用户在获取到Sailing Cloud的安装文件后，需要根据安装包里的内容进行安装，基于master节点和minion节点的差异，安装包里的内容有所不同。
###master节点安装包文件
1. image （存放配置文件的文件夹）
2. deploy-master.sh 
3. deploy_auto_ma 
4. deploy_addone_ali （**后期应该会rename，如改成deploy_addone，现在保留ali的后缀是为了与内网机器上的部署binary进行区分**）
5. clean-and-deploy-master.sh
6. tarpackagema.tar
7. validate_master.sh
8. clean.sh 
###minion节点安装包文件
1. clean.sh
2. deploy-minion.sh 
3. deploy_auto_mi
4. clean-and-deploy-minion.sh 
5. tarpackagemi.tar 
6. validate_minion.sh 

##安装提示
用户在安装过程中，随着步骤依次进展，自动部署脚本会有一些提示语指导你进行安装，下面列出一些常见的安装提示语，并给出解释，用户如果在安装过程中有疑惑，可到**安装提示**来寻求帮助。

| Deploy master node   |    部署master节点 | 
| :-------- | --------| 
| Please input cluster name| 输入集群名称 |  
| Please input user name| 输入用户名 |  
| Please input password| 输入用户密码 |  
|Please input net interface, default eth0| 输入网络接口，默认是etho |  
| Please input public ip| 输入公网ip |  
| Please input your intranet ip| 输入内网ip |  
| Please input data dir where you want to mount registry and etcd, default /mnt|指定存储registry和etcd数据的绝对路径 |  
| Do you want to overwrite the existing cluster name forcely (y/n), default n| 是否重写现有集群名称|  



##master节点安装步骤
###在新环境中开始部署master节点
以root用户权限执行部署脚本，根据提示输入用户指定参数 ，下面安装步骤会提示输入用户名、密码，才能获取镜像安装文件并进行安装。其中用户名和密码是澜云试用版本提供的授权方式，所有注册成功的用户都在后台得到授权。用户名和密码用以登录监控界面。在部署master节点时，请确保充当master节点机器的8080, 8081, 80, 5000, 4001, 4194, 50000,8285,3333端口没有被占用。
```
# ./deploy-master.sh 
Deploy master node
Please input cluster name: 请输入指定的集群名称
Please input user name: 请输入指定用户名
Please input password: 请输入指定用户密码
Please input net interface, default eth0: 请输入内网网卡，默认为eth0
Please input public ip: 请输入外网ip
Please input your intranet ip: 请输入内网ip
Please input data dir where you want to mount registry and etcd: 请输入指定的存储registry与etcd数据的绝对路径
Do you want to overwrite the existing cluster name forcely (y/n):输入y或n，用以确认是否覆写已有的同名集群
```

###重新部署master节点
以root用户权限执行部署脚本，同样需要输入相应参数，后续和在新环境中部署一样。
```
$./clean-and-deploy-master.sh
Deploy master node
Please input cluster name: 请输入指定的集群名称
Please input user name: 请输入指定用户名
Please input password: 请输入指定用户密码
Please input net interface, default eth0: 请输入内网网卡，默认为eth0
Please input public ip: 请输入外网ip
Please input your intranet ip: 请输入内网ip
Please input data dir where you want to mount registry and etcd: 请输入指定的存储registry与etcd数据的绝对路径
Do you want to overwrite the existing cluster name forcely (y/n):输入y或n，用以确认是否覆写已有的同名集群
```

##minion节点安装步骤
###在新环境中部署minion 节点
以root用户权限执行部署脚本，同样需要输入相应参数，用户可设置minion机器的内网IP、用户名等，方便用户对整个机器集群进行管理。请确保充当minion节点机器的4194, 8285端口没有被占用。
```
# ./deploy-minion.sh
Deploy minion node
Please input net interface, default eth0: 请输入内网网卡，默认为eth0
Please input user name: 请输入用户名，与部署master节点时输入的用户名相同
Please input your master intranet ip: 请输入master节点的内网ip

```
###重新部署minion节点
以root用户权限执行部署脚本，同样需要输入相应参数，用户可设置minion机器的内网IP、用户名等，方便用户对整个机器集群进行管理。

```
$./clean-and-deploy-minion.sh
Deploy minion node
Please input net interface, default eth0: 请输入内网网卡，默认为eth0
Please input user name: 请输入用户名，与部署master节点时输入的用户名相同
Please input your master intranet ip: 请输入master节点的内网ip
```
