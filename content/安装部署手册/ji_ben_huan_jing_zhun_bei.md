##基本环境准备
开始部署集群之前，需要在所有的机器上安装好docker环境。ＳailingCloud支持两种docker安装方式：
* 
在线安装docker
* 
离线安装docker

###在线安装docker
推荐用户根据docker官方文档进行在线安装。SailingCloud会率先支持docker最新稳定版本，请确保docker环境部署正常，docker deamon正常启动之后，再进行后续的操作。

###离线安装docker

目前SailingCloud也提供了离线的docker安装方式，要求用户的操作系统是64位的ubuntu14.04或Centos7.0，

*注：Centos安装时注意改变SOFTWARE SELECTION的Minimal Install默认选项，修改为其他选项（**推荐Server with GUI**）将包安装完整（**操作系统包安装不完整可能会导致离线docker安装后使用不稳定**）
*

用户在使用CentOS7以及 Ubuntu 14.04的单机版离线安装包进行安装时，离线安装的步骤如下：
* 
下载好安装包，并且解压之后，
* 
进入到对应的操作系统目录，
* 
之后执行
`./offlineDockerInstall.sh <host ip>`如 `./offlineDockerInstall.sh 10.10.102.28`



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
