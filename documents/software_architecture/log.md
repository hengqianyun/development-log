## 渲染的过程昂贵
1. 挤压导致其他元素计算变化
2. 动画放置于主线程、可能被js代码阻塞

#### 优化
+ requestAnimationFrame ---- 少用
    +   window.requestAnimationFrame() 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行。
    + 当你准备更新动画时你应该调用此方法。这将使浏览器在下一次重绘之前调用你传入给该方法的动画函数(即你的回调函数)。回调函数执行次数通常是每秒60次，但在大多数遵循W3C建议的浏览器中，回调函数执行次数通常与浏览器屏幕刷新次数相匹配。为了提高性能和电池寿命，因此在大多数浏览器里，当requestAnimationFrame() 运行在后台标签页或者隐藏的\<iframe> 里时，requestAnimationFrame() 会被暂停调用以提升性能和电池寿命。
+ 代码拆分，将代码块缩小


## passive ---- 解决触发DOM事件时的阻塞

## DOM 事件监听
>EventTarget.addEventListener() 方法将指定的监听器注册到 EventTarget 上，当该对象触发指定的事件时，指定的回调函数就会被执行。 事件目标可以是一个文档上的元素 Element,Document和Window或者任何其他支持事件的对象 (比如 XMLHttpRequest)。[1]

>addEventListener()的工作原理是将实现EventListener的函数或对象添加到调用它的EventTarget上的指定事件类型的事件侦听器列表中。[1]

#### 语法
target.addEventListener(type, listener, options);
target.addEventListener(type, listener, useCapture);
1. preventDefault




## 参考
>[1] MDN Web Docs [EventTarget.addEventListener()](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener)