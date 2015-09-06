
##minion节点部署

###在新环境中部署minion 节点
以root用户权限执行部署脚本，同样需要输入相应参数，用户可设置minion机器的内网IP、用户名等，方便用户对整个机器集群进行管理。请确保充当minion节点机器的4194, 8285端口没有被占用。
```
# ./deploy-minion.sh
Deploy minion node
Please input net interface, default eth0: 
Please input user name: 
Please input your master intranet ip: 

```
###重新部署minion节点
以root用户权限执行部署脚本，同样需要输入相应参数，用户可设置minion机器的内网IP、用户名等，方便用户对整个机器集群进行管理。

```
$./clean-and-deploy-minion.sh
Deploy minion node
Please input net interface, default eth0: 
Please input user name: 
Please input your master intranet ip: 
```