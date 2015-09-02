#安装部署手册 
用户在使用SailingCloud提供的跨云端应用运维管理服务之前，需要进行平台安装和部署等前期准备工作，用户可先访问[SailingCloud官网](http://10.10.105.72:8800/)，先注册帐号，并访问SailingCloud提供的平台安装文件获取地址。

澜云提供安全的公有镜像供用户使用，用户不需要专业的安装技术，通过澜云提供的自动化安装脚本，用户只需几行简单命令，即可完成安装。  

##基本环境准备


###离线安装docker

开始部署集群之前，需要在所有的机器上安装好docker环境，我们提供了离线的docker安装方式，目前我们提供CentOS （CentOS7.x或以上）以及 Ubuntu 14.04的单机版离线安装包，离线安装的步骤如下：
* 
下载好安装包，并且解压之后，
* 
进入到对应的操作系统目录，
* 
之后执行
`./offlineDockerInstall.sh <host ip>`如 `./offlineDockerInstall.sh 10.10.102.28`


###在线安装docker
还可以根据docker官方文档进行在线安装。
请确保docker环境部署正常，docker1 deamon正常启动之后，在进行后续的操作。

###镜像下载
在部署集群之前，需要把集群部署需要的组件提前下载好，已注册的用户可以通过安装包中的 ./deploy_download 客户端，可以直接将master节点和minion节点所需要的镜像包下载下来：`./deploy_download -u=<username> -p=<password>`。并且自行将minion节点需要的tar包分发到各个节点上。

###镜像安装文件
用户在获取安装文件后，需要根据安装包里的内容进行安装，master节点和minion节点的镜像安装文件存在差异，安装包里的内容有所不同。下面列出master节点和minion节点的安装包文件对比表，用户在获取安装文件后，可比对该表核查安装文件的完整性。

|master节点安装包文件   | minion节点安装包文件  |
| :-------- | :--: |
| image  |    |
| deploy-master.sh   |  deploy-minion.sh    |
| deploy_auto_ma   |  deploy_auto_mi  |
| deploy_addone_ali   |   |
|  clean-and-deploy-master.sh |   clean-and-deploy-minion.sh    |
|  tarpackagema.tar |  tarpackagemi.tar   |
|  validate_master.sh| validate_minion.sh  |
|  clean.sh |  clean.sh   |

### 安装说明
用户在下载镜像文件后,在安装之前，有几点需要说明，用户在自己的机器上指定一台可连接外网的机器作为master node,master node节点的机器作为整个机器集群的中枢，承担着连接内外网的媒介作用，需要为master节点的机器设置外网IP,minion节点机器支持离线功能。master节点对机器的硬件性能要求较高，要求承担master node的机器具备4核、8G内存和至少50g的硬盘空间。此外，若干台作为minion node。然后安装部署Docker及相应组件。安装镜像的情景主要有两种，用户可根据具体情景进行安装,主要情景有：
1. **在一个新环境中开始部署**
2.  **重新部署master节点**




##master节点部署
###安装提示
用户在安装过程中，随着步骤依次进展，自动部署脚本会有一些提示语指导你进行安装，下面列出一些常见的安装提示语，并给出解释，用户如果在安装过程中有疑惑，可到安装提示来寻求帮助。

| 安装提示语   |  解释   | 
| :-------- | --------| 
| Deploy master node   |    部署master节点 | 
| Please input cluster name| 输入集群名称 |  
| Please input user name| 输入用户名 |  
| Please input password| 输入用户密码 |  
|Please input net interface, default eth0| 输入网络接口，默认是etho |  
| Please input public ip| 输入公网ip |  
| Please input your intranet ip| 输入内网ip |  
| Please input data dir where you want to mount registry and etcd, default /mnt|指定存储registry和etcd数据的绝对路径 |  
| Do you want to overwrite the existing cluster name forcely (y/n), default n| 是否重写现有集群名称|  

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

##minion节点部署
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
##故障处理
如果在集群运维过程中出现问题，可以尝试通过validate _ master.sh  以及 validate _ minion.sh判断组件运行是否正常，如果组件一切运行正常，通过界面仍然无法正常操作，请联系客服，如果组件运行故障，可以尝试以下方式重启组件，如果仍无法恢复，请联系客服。下表列出了一些常见故障问题及解决方案。

首先请确认组件是否存在异常，可根据退出码进行判断：
* 
** 如果退出码为0，则重启该组件**
* 
**如果退出码不为0，请联系客服。**


用户可按下面的方法对问题组件进行排查：
* 
etcd组件问题 ：通过以下命令检查运行状态
$ docker -H unix:///var/run/docker-bootstrap.sock ps | grep etcd 
假设名为infra0的组件退出，且退出码为0，则执行
$ docker -H unix:///var/run/docker-bootstrap.sock restart infra0
假设该组件异常退出，请联系客服

* 
monit server ：通过以下命令检查运行状态
$ docker ps | grep monitserver
假设该组件退出码为0，则执行
$ docker start $(docker ps | grep monitserver | awk '{print $1}') 
假设组件异常退出，请联系客服。

* 
gorouter： 检查运行状态
$ docker ps | grep gorouter
假设该组件退出码为0，则执行
$ docker start $(docker ps | grep gorouter | awk '{print $1}') 
假设组件异常退出，请联系客服。

 




