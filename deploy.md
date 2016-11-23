## 切换管理员帐号：
`sudo su -`

## 启动mongodb: 
`cd /storage/mongodb && ./mongod --config ./mongodb.conf &`

## 启动redis：
`cd /usr/local/bin && ./redis-server &`

## 启动fete：
`cd ~/service/fete && pm2 start server.js`

## 启动旧接口(iwfe)：
`cd ~/service/iwfe && pm2 start server.js`

## 启动ajax抓包项目：
`cd ~/service/git/ajax_log && pm2 start bin/run`

## 启动博客：
`cd ~/service/ghost && forever start index.js` (目前因为sqlite3的包装不上，无法启动)

## 启动npm仓库
`docker ps -a`  
查看名字叫 sinopia 的容器 ID  
`docker start <sinopia 的容器 ID>`  
注意：不要使用 `docker run` 命令，如果不小心使用了 `docker run` 命令来启动，会导致 npm 仓库上之前的数据都不在。补救方法：使用  `docker inspect sinopia`
命令查看之前 sinopia 数据存放位置，类似：   
 
```json  
"Mounts": [
	{
	    "Source": "/root/sinopia/config.yaml",
	    "Destination": "/opt/sinopia/config.yaml",
	    "Mode": "",
	    "RW": true,
	    "Propagation": "rprivate"
	},
	{
	    "Name": "05998af7b79b775bddee14bb81e87a2b57e61501f83724e8ad083ff428f11642",
	    "Source": "/var/lib/docker/volumes/05998af7b79b775bddee14bb81e87a2b57e61501f83724e8ad083ff428f11642/_data",
	    "Destination": "/opt/sinopia",
	    "Driver": "local",
	    "Mode": "",
	    "RW": true,
	    "Propagation": ""
	}
],
```  

在 `/var/lib/docker/volumes/` 下找到之前的数据存放位置替换旧行了

## 启动jenkins
`docker ps -a`  
查看名字叫 jenkins_server 的容器 ID  
`docker start <jenkins_server 的容器 ID>`