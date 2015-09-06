
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
Please input cluster name: 
Please input user name: 
Please input password: 
Please input net interface, default eth0: 
Please input public ip: 
Please input intranet ip: 
Please input directory where you want to store application data, default /mnt: 
How long do you prefer to store application log, counted by day, default 1: 
Do you want to overwrite the existing cluster name forcely (y/n), default n: 
```

###重新部署master节点
以root用户权限执行部署脚本，同样需要输入相应参数，后续和在新环境中部署一样。

```
$./clean-and-deploy-master.sh
Deploy master node
Please input cluster name: 
Please input user name: 
Please input password: 
Please input net interface, default eth0: 
Please input public ip: 
Please input your intranet ip: 
Please input data dir where you want to mount registry and etcd: 
Do you want to overwrite the existing cluster name forcely (y/n):
```