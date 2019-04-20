---
title: 使用 Verdaccio 搭建npm私有仓库
date: 2019-04-20 10:51:18
tags:
  - verdaccio
  - npm 
  - 私有库
categories:
  - verdaccio
  - npm 
keywords:
  - verdaccio
  - npm 
autoThumbnailImage: false
thumbnailImagePosition: "bottom"
thumbnailImage: https://verdaccio.org/docs/assets/logo/banner/png/verdaccio-banner@3x.png
coverImage: http://d1u9biwaxjngwg.cloudfront.net/welcome-to-tranquilpeak/city.jpg
metaAlignment: center
comments: true

---
[![996.icu](https://img.shields.io/badge/link-996.icu-red.svg)](https://996.icu)
### Verdaccio 是什么？
  Verdaccio 是一个轻量的私有npm proxy registry。
<!-- more -->
### Verdaccio有哪些特点？

* Verdaccio 支持 npm、yarn和npnm等主流的npm客户端
* 支持Docker和 Kubernetes Helm部署
* Verdaccio 是基于插件的，支持身份验证、中间件和存储插件


### 服务器上安装

**最低要求:**
* Node.js 版本
  对于 verdaccio@3.x 版本，Node v6.12. 是最低支持版本。
  对于 verdaccio@4.0.0-alpha.x 或 verdaccio@4.x版本， Node 8.x (LTS "Carbon") 是最低支持版本。
* npm >=4.x 或 yarn > 我们强烈建议使用最新的 Node 包管理客户端 > npm@5.x | yarn@1.x | pnpm@2.x
* Web 界面支持 Chrome, Firefox, Edge, 和 IE11 浏览器。

###### 安装Verdaccio CLI
###### 1、 npm进行 全局安装:

  ```javascript
    npm install -g verdaccio --unsafe-perm
  ```
  **加上--unsafe-perm选项是为了防止gyp ERR! permission denied权限问题报错**

  ![服务器安装verdaccio](/assets/images/verdaccio1.png)

###### 2、使用[ln](http://man.linuxde.net/ln)命令给 verdaccio 配置“快捷方式”:
``
  ln -s /app/node-v10.15.0-linux-x64/lib/node_modules/verdaccio/bin/verdaccio /usr/local/bin/verdaccio
``
  
  ![ln](/assets/images/verdaccio2.png)

###### 3、 运行 verdaccio:
  ``
  verdaccio
  ``

  ![verdaccio](/assets/images/verdaccio3.png)


*  config file 默认配置文件路径位置([更多配置信息](https://verdaccio.org/docs/zh-CN/configuration))
*  Plugin successfully 插件加载信息
*  http address 默认访问地址

###### 4、在config.yaml配置中添加 listen 配置:
 ![verdaccio](/assets/images/verdaccio6.png)

###### 5、 使用 [pm2](https://www.npmjs.com/package/pm2) 守护 verdaccio 进程

###### 6、 访问搭建好的私有仓库:
  在浏览器中访问 https://你的服务器外网IP:4873
  ![verdaccio](/assets/images/verdaccio8.png)
  能访问到这个界面说明部署成功了

###### 7、 注册登录 verdaccio:
  执行命令
  ``
  npm adduser --registry  http://118.24.154.202:4873
  ``

  ![verdaccio](/assets/images/verdaccio10.png)

###### 8、 在本地创建一个npm包然后执行:
  ``
  npm publish --registry http://118.24.154.202:4873
  ``

  ![verdaccio](/assets/images/verdaccio11.png)

###### 9、 刷新仓库页面，你就能看就你上传的 npm 包，这样你的私有库就部署成功了！
  ![verdaccio](/assets/images/verdaccio12.png)




  


