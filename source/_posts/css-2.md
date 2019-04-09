---
layout: post
title: chrome input autofill 自动填充背景色问题 
author: CAO qisen
date: 2017-03-04 23:17:52
subtitle:
header-img:
cdn:
tags: 
    - CSS
    - chrome
    - input
---
在[stackoverflow](http://stackoverflow.com/questions/2781549/removing-input-background-colour-for-chrome-autocomplete)发现解决方法如下：
## 方法一：box-shadow
```css
input:-webkit-autofill {
    -webkit-box-shadow: 0 0 0px 1000px white inset;
}
```
### box-shadow: h-shadow v-shadow blur spread color inset;
<!-- excerpt -->
box-shadow的作用是给盒子添加一个阴影。参数如下：

| 参数        | 是否必选    |  描述  |
| --------    | -----:   | :----: |
| h-shadow| 必选|水平阴影的位置，可以为负|
| v-shadow| 必选|垂直阴影的位置，可以为负|
| blur|可选|模糊距离|
| spread|可选|阴影尺寸|
| color|可选|阴影颜色|
| inset|可选|设置后将外部阴影设置为内部阴影|

这种方式实际上是通过给input框内部添加一个指定颜色阴影的方式达到设置input背景色的视觉效果。
但是，如果需求是input的背景颜色透明呢？
## 方法二：animation
```css
@-webkit-keyframes setbackgroundcolor {
    to {
        background: transparent;
    }
}

input:-webkit-autofill {
    -webkit-animation-name: setbackgroundcolor;
    -webkit-animation-fill-mode: forwards;
}
```
这种方式为input:-webkit-autofill绑定了一个动画效果setbackgroundcolor，并将其填充模式(fill-mode)设置为forwards(保留动画结束后的效果)。
标签绑定动画后，若不指定动画时长animation-duration，将无法看到动画的播放效果而直接完成动画。
这里直接将动画效果设为背景色透明，指定填充模式为forwards，相当于将input:-webkit-autofill的背景重设成了透明。

参考链接：
http://stackoverflow.com/questions/2781549/removing-input-background-colour-for-chrome-autocomplete
http://www.w3school.com.cn/cssref/pr_box-shadow.asp
http://www.w3school.com.cn/cssref/pr_animation-name.asp
http://www.w3school.com.cn/cssref/pr_animation-duration.asp
http://www.w3school.com.cn/cssref/pr_animation-fill-mode.asp