---
layout: post
title: RESTful API
author: CAO qisen
date: :year/:month/:day/
subtitle:
header-img:
cdn:
tags:
    - REST
---

#### 什么是REST ？
>   REST（Representational State Transfer）翻译为表现层状态转换，是Roy Thomas Fielding博士于2000年在他的博士论文中提出来的一种万维网软件架构风格，目的是便于不同软件/程序在网络（例如互联网）中互相传递信息。表现层状态转换是根基于超文本传输协议(HTTP)之上而确定的一组约束和属性，是一种设计提供万维网络服务的软件构建风格。匹配或兼容于这种架构风格(简称为 REST 或 RESTful)的网络服务，允许客户端发出以统一资源标识符访问和操作网络资源的请求，而与预先定义好的无状态操作集一致化。因此表现层状态转换提供了在互联网络的计算系统之间，彼此资源可交互使用的协作性质(interoperability)。相对于其它种类的网络服务，例如 SOAP服务则是以本身所定义的操作集，来访问网络上的资源。
>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    ——摘自维基百科

<!-- excerpt -->
#### REST是设计风格
> REST通常基于使用HTTP，URI，和XML以及HTML这些现有的广泛流行的协议和标准。

* 资源是由URI来指定。
* 对资源的操作包括获取、创建、修改和删除资源，这些操作正好对应HTTP协议提供的GET、POST、PUT和DELETE方法。
* 通过操作资源的表现形式来操作资源。
* 资源的表现形式则是XML或者HTML，也可以是任何其他的格式。</font> 

### RESTful API
> 匹配REST设计风格的Web API称为RESTful API。它从以下三个方面资源进行定义：

* 直观简短的资源地址：URI，比如：http://xxx.com/resources/。
* 传输的资源：Web服务接受与返回的互联网媒体类型，比如：JSON, XML, YAML等。
* 对资源的操作：Web服务在该资源上所支持的一系列请求方法（比如：POST，GET，PUT或DELETE）。


### HTTP请求方法在RESTful API中的应用

| 资源 | GET | PUT | POST | DELETE |
| :-: | :--: | :--: | :--: | :-: |
|<font size=2 >一组资源的URI，比如https://xxx.com/resources/	|<font size=2.5 >列出URI，以及该资源组中每个资源的详细信息。|	<font size=2.5 >使用给定的一组资源替换当前整组资源。|	<font size=2.5 >在本组资源中创建/追加一个新的资源。该操作往往返回新资源的URL。|	<font size=2.5 >删除整组资源。|
|<font size=2.5 >单个资源的URI，比如https://xxx.com/resources/142|	<font size=2.5 >获取指定的资源的详细信息，格式可以自选一个合适的网络媒体类型（比如：XML、JSON等）|	<font size=2.5 >替换/创建指定的资源。并将其追加到相应的资源组中。|<font size=2.5 >	把指定的资源当做一个资源组，并在其下创建/追加一个新的元素，使其隶属于当前资源。|	<font size=2.5 >删除指定的元素。|

### REST的优点
* 可更高效利用缓存来提高响应速度
* 通讯本身的无状态性可以让不同的服务器的处理一系列请求中的不同请求，提高服务器的扩展性
* 浏览器即可作为客户端，简化软件需求
* 相对于其他叠加在HTTP协议之上的机制，REST的软件依赖性更小
* 不需要额外的资源发现机制在软件技术演进中的长期的兼容性更好