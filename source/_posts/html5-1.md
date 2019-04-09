---
layout: post
title: "HTML5.1 响应式图像"
subtitle: "HTML5.1新属性 srcset、sizes、picture的用法"
date: 2017-02-19 23:15:48
author: "CAO qisen"
## header-img: "img/post-default.jpg"
cdn: 'header-on'
tags:
	- html5.1
  - srcset
  - sizes
  - picture
---
## HTML5.1 响应式图像

W3C 引入了一些功能特性，无需使用 CSS 就可以实现响应式图像。它们是 …
### srcset 图像属性

srcset 属性让你可以指定一个多个可选的图像来源，对应于不同的像素分辨率。它将允许浏览器根据用户设备的不同选择合适质量的实现来进行显示。例如，对于使用网络比较慢的移动设备的用户，显示一张低分辨率的图片会比较好。
<!-- excerpt -->
你可以使用 srcset 属性并且带上它自有的 x 修饰符来描述每一个图片的像素比例, 如果用户的像素比例等于 3，就会显示 high-res 这张图片。
```html
<img src="clicks/low-res.jpg" srcset="
  clicks/low-res.jpg 1x, 
  clicks/medium-res.jpg 2x, 
  clicks/high-res.jpg 3x"
>
```
除了像素比例之外，你也可以选择使用 w 修饰符来指定不同尺寸大小的图片。在如下示例中，high-res 图片被定义成在宽度为 1600px 时显示。
```html
<img src="clicks/low-res.jpg" srcset="
  clicks/low-res.jpg 500w, 
  clicks/medium-res.jpg 1000w, 
  clicks/high-res.jpg 1600w"
>
```

### sizes 图像属性

大多数时候创作者们都喜欢针对不同的屏幕尺寸显示不同的图片。这个可以用 sizes 属性做到。它让你可以针对分配给图像显示的空间大小来对宽度做出调整, 然后使用 srcset 属性来挑选合适的图片来显示。例如…
```html
<img src="clicks/low-res.jpg" sizes="(max-width: 25em) 60vw, 100vw" 
  srcset="clicks/low-res.jpg 500w, 
  clicks/medium-res.jpg 1000w, 
  clicks/high-res.jpg 1600w"
>
```
在这里， sizes 属性定义了在视窗大于 25 em 时图像宽度为视窗宽度的 100%，或者在小于等于 25em 时为视图宽度的 60%。
### picture 元素

picture 元素让你可以针对不同的屏幕尺寸声明图片。这个可以通过用 <picture> 元素封装 <img> ，并且描述多个 <source> 子元素来实现。

<picture> 标记单独使用并不会显示任何东西。你已经被假定会声明默认的图像来源作为  src 属性的取值，而可选的图像来源则会放在 scrset 属性之中，如下所示：
```html
<picture>
  <source media="(max-width: 25em)" srcset="
    clicks/small/low-res.jpg 1x,
    clicks/small/medium-res.jpg 2x, 
    clicks/small/high-res.jpg 3x
  ">
  <source media="(max-width: 60em)" 
    clicks/large/low-res.jpg 1x,
    clicks/large/medium-res.jpg 2x, 
    clicks/large/high-res.jpg 3x
  ">
 
  <img src="clicks/default/medium-res.jpg">
</picture>
```