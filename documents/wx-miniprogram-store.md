#小程序Store实现

##核心问题

1.state值修改时如何获取当前页面并触发setData
2.~~如若不将state注入至data中，如何优雅的在.wxml中使用插值~~
3.~~如何将setData抽离，优雅地触发store的setState~~


##参考插件
[微信小程序实现store功能](https://blog.csdn.net/milugloomy/article/details/102609414)

###插件思路

>创建store，覆写Page和Component生命周期，在onload中将state注入到data中，添加当前this入页面栈，挂载setState方法。setState接收参数于setData相同，遍历页面栈，依次调用setData。在unOnload将当前页面出栈。

###缺点
>由于小程序架构问题，导致diff的触发需要setData，且无法设置组件缓存，相较直接链接Dom，多了一层通信，延迟变高。这个实现方式并非创建了状态管理器，而是创建了一个全局的mixin。数据的模块划分也不够明确。

###优化
>采用依赖注入，为store添加module



