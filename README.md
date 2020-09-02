你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
crontab
=======

A crontab tool build by golang

# Crontab

## 背景：
       
在实际工作中经常需要在服务器上添加定时任务，当任务多了的时候管理起来就比较麻烦，所以想要有一个方便使用和管理的crontab工具

## 功能介绍：
       
使用web api的方式提供任务的添加、删除、查看、运行状态、暂停、恢复、重新加载配置、日志查看等功能，清晰的任务执行日志和工具的系统日志便于问题查找和任务监控。

## 使用：

* ./crontab -h
* Usage of ./crontab:
* -conf="crontab.conf": crontab config
* -logs="logs/": log path
* -port=":8080": web port

## crontab.conf格式

`{"time":"* * * * *","cmd":"php","args":["-v"],"out":"./logs/php_v.log","comment":"备注"}`

每一行为一个json对象，字段说明：
* time:任务执行时间，参考linux crontab
* cmd:可执行程序
* args:可执行程序参数
* out:执行输出文件
* comment:任务备注

同样适用于api的job字段

## API：

|api|说明|
|---|---|
|/get|获取当前设置的任务列表  json|
|/set?h=key&j=job| 设置一个键值为key的任务/修改一个键值为key的任务（h为空或者不设置时，key=md5(job)）|
|/del?h=key       |删除键值为key的任务，下次不再执行|
|/log?d=20141228  |获取d天的任务运行日志|
|/load            |重新加载配置文件，可以手动修改配置文件之后调用重新加载而不重启服务|
|/stop            |停止，已经在执行的任务继续执行，停止触发后续任务执行|
|/start           |开始，继续触发任务执行|
|/status          |获取当前正在执行的任务，包括进程ID、任务信息、任务开始时间信息  json|

## 规划功能：

* 添加邮箱报警功能、当任务执行失败，出错等及时邮箱报警

