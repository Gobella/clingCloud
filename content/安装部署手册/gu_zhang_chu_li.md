##故障处理

如果在集群运维过程中出现问题，可以尝试通过validate _ master.sh  以及 validate _ minion.sh判断组件运行是否正常，如果组件一切运行正常，通过界面仍然无法正常操作，请联系客服，如果组件运行故障，可以尝试以下方式重启组件，如果仍无法恢复，请联系客服。下表列出了一些常见故障问题及解决方案。

首先请确认组件是否存在异常，可根据退出码进行判断：
* 
** 如果退出码为0，则重启该组件**
* 
**如果退出码不为0，请联系客服**


用户可按下面的方法对问题组件进行排查：
* 
etcd组件问题 ：通过以下命令检查运行状态
```$ docker -H unix:///var/run/docker-bootstrap.sock ps | grep etcd``` 
假设名为infra0的组件退出，且退出码为0，则执行
```$ docker -H unix:///var/run/docker-bootstrap.sock restart infra0```
假设该组件异常退出，请联系客服

* 
monit server ：通过以下命令检查运行状态
```$ docker ps | grep monitserver```
假设该组件退出码为0，则执行
```$ docker start $(docker ps | grep monitserver | awk '{print $1}') ```
假设组件异常退出，请联系客服。

* 
gorouter： 检查运行状态
```$ docker ps | grep gorouter```
假设该组件退出码为0，则执行
```$ docker start $(docker ps | grep gorouter | awk '{print $1}')``` 
假设组件异常退出，请联系客服。
