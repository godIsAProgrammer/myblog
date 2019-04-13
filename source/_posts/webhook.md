---
title: "webhook配合node.js实现简单的自动化部署"
date: "2019-04-11"
categories:
  - webhook
  - nodejs
  - github
tags:
  - webhook
  - github
  - node.js
keywords:
  - webhook
  - github
  - node.js
autoThumbnailImage: false
thumbnailImagePosition: "bottom"
thumbnailImage: http://d1u9biwaxjngwg.cloudfront.net/welcome-to-tranquilpeak/city-750.jpg
coverImage: http://d1u9biwaxjngwg.cloudfront.net/welcome-to-tranquilpeak/city.jpg
metaAlignment: center
comments: true

---
[![996.icu](https://img.shields.io/badge/link-996.icu-red.svg)](https://996.icu)
### 什么是webhook？
  webhook（也称为Web回调或HTTP推送API）是应用程序为其他应用程序提供实时信息的一种方式。 webhook会在发生时将数据传递给其他应用程序，这意味着可以立即获取数据。与典型的API不同，你不需要非常频繁地轮询数据才能实时获取数据。这使得webhooks对提供者和消费者都更有效。 

   <!-- more -->

了解完webhook之后，我们就开始利用webhook实现简单的自动化部署了。
这里我们以GitHub的项目作为🌰

#### 1、登录GitHub -> 进入项目 -> Settings (项目设置) -> Webhooks

**Payload URL:**
  当你向GitHub push代码时，GitHub会向Payload URL里填写的URL发送POST请求，其中包含任何订阅事件的详细信息。你还可以指定要接收的数据格式（JSON，x-www-form-urlencoded等）。更多信息可以查看[developer documentation](https://developer.github.com/webhooks/)。
  
![github webhook settings](/assets/images/webhook-1.png)

#### 2、登录服务器
#### 3、安装[github-webhook-handler](https://www.npmjs.com/package/github-webhook-handler)依赖 

```
npm i github-webhook-handler
```
**注意：** 在Github Webhooks 设置里, Content type 必须为 application/json.

#### 4、创建处理webhook的脚本

``` javascript
// gitupdate.js

var http = require('http')
var createHandler = require('/usr/bin/node_modules/github-webhook-handler')
var handler = createHandler({ path: '/webhook', secret: 'xxx' })

function run_cmd(cmd, args, callback) {
  var spawn = require('child_process').spawn;
  var child = spawn(cmd, args);
  var resp = "";

  child.stdout.on('data', function(buffer) { resp += buffer.toString(); });
  child.stdout.on('end', function() { callback (resp) });
}

http.createServer(function (req, res) {
  handler(req, res, function (err) {
    res.statusCode = 404
    res.end('no such location')
  })
}).listen(7777)

handler.on('error', function (err) {
  console.error('Error:', err.message)
})

handler.on('push', function (event) {
console.log(1111)
  console.log('Received a push event for %s to %s',
    event.payload.repository.name,
    event.payload.ref)
    run_cmd('sh', ['./deploy.sh',event.payload.repository.name], function(text){ console.log(text) });
})

handler.on('issues', function (event) {
  console.log('Received an issue event for %s action=%s: #%d %s',
    event.payload.repository.name,
    event.payload.action,
    event.payload.issue.number,
    event.payload.issue.title)
})

```

**注意：** secret字段内容必须与在Github Webhooks设置里secret上所填的内容一致。

#### 5、创建处理git命令的脚本

```bash
// deploy.sh

WEB_PATH='/root/tools/'$1
WEB_USER='root'
WEB_USERGROUP='root'

echo "Start deployment"
cd $WEB_PATH
echo "pulling source code..."
git reset --hard origin/master
git clean -f
git pull
git checkout master
echo "changing permissions..."
chown -R $WEB_USER:$WEB_USERGROUP $WEB_PATH
echo "Finished."
```

**注意:** 1、WEB_PATH是你的项目所在路径；2、$1为run_md方法里传进来的仓库名称；


#### 6、运行gitupdate.js
```javascript
node gitupdate.js
```
**注意:** 要想进程在后台运行，可安装[pm2](https://www.npmjs.com/package/pm2)守护进程。



