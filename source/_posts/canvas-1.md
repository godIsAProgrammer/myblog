---
title: canvas 绘制环形进度条
date: 2017-03-14 22:56:34
categories:
    - canvas
tags:
    - canvas
    - html5
    - 进度条
keywords:
    - canvas
autoThumbnailImage: true
thumbnailImagePosition: "bottom"
#thumbnailImage: http://d1u9biwaxjngwg.cloudfront.net/welcome-to-tranquilpeak/city-750.jpg
#coverImage: http://d1u9biwaxjngwg.cloudfront.net/welcome-to-tranquilpeak/city.jpg
metaAlignment: center
---

 最近工作上有遇到绘制环形进度条的需求，绘制环形进度条可以由传统的css3和canvas实现，这边介绍的是canvas的实现方式。
 <!-- excerpt -->
```html
    <-- html部分 -->
    <canvas class="process" width="300" height="300" data-process="10"></canvas>
```
```javascript
    // javascript 部分
    var canvas = document.getElementsByClassName('process');  // 获取 canvas对象
    var ctx = canvas.getContext('2d'); // 拿到笔触
    var process = canvas.getAttribute('data-process'); // 要绘制的百分比
    var x = canvas.width / 2;
    var y = canvas.height / 2;
    var r = canvas.height / 2;
    drawArc(ctx, x, y, r, process, '#F6F6F6', '#FF9600', '#fff', '#333', 100 );
    
    // ctx : 笔触 ， bgColor：要填充的背景色 ， processColor：进度色， fillColor：内圆填充色
    // tColor：内圆文字颜色，fSize：内圆字体大小，process：百分百 
    function drawArc (ctx, x, y, r, process, bgColor, processColor, fillColor, tColor, fSize) { 
        // 背景圆
        ctx.beginPath();
        ctx.arc(x, y, r, 0, Math.PI * 2);
        ctx.closePath();
        ctx.fillStyle = bgColor; //'#F6F6F6';
        ctx.fill();

        // 进度条
        ctx.beginPath();
        ctx.moveTo(x, y);  
        ctx.arc(x, y, r, Math.PI * 1.5, Math.PI * (1.5 + 2 * process / 100));
        ctx.closePath();
        ctx.fillStyle = processColor; // '#FF9600';
        ctx.fill();

        // 画内填充圆
        ctx.beginPath();
        ctx.arc(x, y, 140, 0, Math.PI * 2);
        ctx.closePath();
        ctx.fillStyle = fillColor; // '#fff';
        ctx.fill();

        // 填充文字
        ctx.fillStyle = tColor; // '#333';
        ctx.textAlign = 'center';  
        ctx.textBaseline = 'middle';  
        ctx.font= fSize +　'px' + ' Arial';
        ctx.moveTo(x, y);  
        ctx.fillText(process + '%', x, y);
    }
```

```javascript
    // 涉及的到 arc()方法
    context.arc(x ,y , r, sAngle, eAngle, counterclockwise);
```