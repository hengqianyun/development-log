# HTML、CSS、JavaScript三者之间的关系

describe

## 前言
> 作为前端开发，我们以前的主要开发环境是website client。网页是一种可视化的表现形式，浏览器环境下，我们用树形文档的结构去描述一个网页，这就是HTML。但是单纯的文档模式，是无法满足的，他们需要各种各样的style，我们想要控制他们的样式，CSS做的便是这一件事。然后我们希望这些结构拥有自己的逻辑和行为，JavaScript变成为了逻辑层。

> JavaScript并不是天然就和HTML在一起的，它是一种脚本语言，用来控制HTML。想要控制并不在一个空间的东西，就需要建立连接，而这个连接的开销是昂贵的。为了建立连接，client抛给了我们一些API，我们称为DOM，文档对象。通过DOM我们就能获取操作HTML的节点了。

> DOM遵循W3C协议，即所有游览器的公约，也就是我们常用的document对象。
> BOM是浏览器对象，由各家浏览器定义，各API稍有区别。

## 什么是HTML
## 什么是CSS
## 什么是JavaScript
## 总结

## 理解浏览器
![client](/assets/software_architecture/client.png)
>红框内便是我们能通过代码操作的部分
>图片取自[Chrome 浏览器架构](https://xie.infoq.cn/article/5d36d123bfd1c56688e125ad3)

#### 对前端而言浏览器是如何工作的

>浏览器目前只了解过Chrome，这里不提及Chrome的工作原理，若有兴趣，可以只看去[Inside look at modern web browser (part 1) ](https://developers.google.com/web/updates/2018/09/inside-browser-part1),总共四个part，也包含了页面渲染的解释。


# 从浏览器渲染过程理解HTML、CSS、JavaScript

## 转化DOM
> 当地址栏发生变化时，chrome开始接收HTML字符数据，然后将数据转化为DOM。

> DOM 是一种浏览器内部用于表达页面结构的数据，同时也为 Web 开发者提供了操作页面元素的接口，让 web 开发者可以在 Javascript 代码中获取和操作页面中的元素。

## 加载资源
> 一个网站通常还会使用类似图片，样式文件和 JavaScript 代码等额外的资源。这些资源从网络或者缓存中获取。