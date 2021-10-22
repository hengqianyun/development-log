# DOM事件监听

`EventTarget.addEventListener(type, Listener, ?options)`
`EventTarget.onclick = function() {/* code */}`

TODO
vue事件解析
passive的应用场景
箭头函数中的this


## 什么是事件绑定

HTML定义了一下行为，当这些行为在网页上发生时，用以触发开发者的逻辑。

## 为什么需要这些事件

用来监听用户的行为，为某些定义的行为添加交互逻辑。

## 两种绑定方式的区别

1. addEventListener是EventTarget的方法，onclick等是GlobalEventHandlers对象的属性，这个对象是一个全局混入对象，无法额外创建实例。
2. 使用方式
    + onclick
    ``` javascript
        document.querySelector('.selector').onclick = function() {/* do stuff */}
    ```
    ...or 直接写于行内
    ``` HTML
        <div onclick="handleClick()"></div>
        <div onclick="alert('handle clicked')"></div>
    ```
    + addEventListener
    ```javascript
        document.querySelector('.selector').addEventListener('click', function() {/* do stuff */})

        const handleClick = function() {/* do stuff */}
        document.querySelector('.selector').addEventListener('click', handleClick)
    ```
3. 一个DOM对象的onclick仅会存在一个，多次绑定也仅会触发最后赋值的那个函数
    ```javascript
        document.querySelector('.selector').onclick = function() {console.log('clicked')} // clicked
        document.querySelector('.selector').onclick = function() {console.log('clicked2')} // clicked2
    ```
    ...而addEventListener可以绑定多个
    ```javascript
        document.querySelector('.selector').addEventListener('click', function() {
            console.log('addEventListener')
        })
        // addEventListener
        document.querySelector('.selector').addEventListener('click', function() {
            console.log('addEventListener2')
        })
        // addEventListener addEventListener2
    ```
    ...当我们需要的是在某种情况下覆盖掉上次绑定的方法，那么就需要`removeEventListener(type, Listener)`
    ```javascript
        const handleClick = function() {/* do stuff */}
        document.querySelector('.selector').addEventListener('click', handleClick)

        document.querySelector('.selector').remvoeEventListener('click', handleClick)
    ```
    ...由于`removeEventListener`第二个参数接收的是对应`type`的监听函数，那么为了能够移除，这个函数就需要是一个可引用的值，即在调用addEventListener的时候，执行函数就不能是匿名函数，而是一个可引用的外部函数。
4. GlobalEventHandlers定义的方法，都是简单易操作的，一个DOM对象有且只能存在一个onclick，触发时会直接通知监听器执行逻辑，进入到主线程中。而addEventListener则有更多的可控性。

## addEventListener

#### options

一个指定有关 listener 属性的可选参数对象。
+ `capture`: `Boolean`  事件的发生默认是在“目标阶段”，当设置为`true`时，表示`listener`会在该类型的事件[捕获阶段](#eventFlow)传播到该`EventTarget`
+ `once`: `Boolean` 设置为`true`时，当`listener`触发后，便会自动移除。
+ `passive`: `Boolean` 设置为`true`时，表示`listener`永远不会调用`preventDefault()`。如果`listener`仍然调用了这个函数，客户端将会忽略它并抛出一个控制台警告。

#### 事件监听的观察者模式
已知DOM连接会带来很大的开销，当我们有一个列表，列表下每一个item都有相同的点击事件。

```html
    <ul>
        <li>one</li>
        <li>two</li>
        <li>three</li>
        <li>four</li>
        <li>five</li>
    </ul>
    <script>
        const li = document.querySelectorAll('li')
        const listener = function() {}
        li.forEach(el => el.addEventListener('click', listener))
    </script>
```
...这是我们的效率是不高的，若`listener`还是一个匿名函数
```javascript
    li.forEach(el => el.addEventListener('click', () => {]}))
```
...此时我们还会面临内存的困扰。
参考观察者模式，我们可以只在`ul`上添加`listener`,以此来减少开销
```javascript
    const ul = document.querySelector('ul')
    ul.addEventListener('click', function(event) {
        if (event.target === 'li') {
            /* do stuff */
        }
    })
```
当我们在使用框架的时候，以vue为例
```HTML
    <ul>
        <li v-for="item, index of list" :key="item.id" @click="handleClick(item.id)">{{item.lable}}</li>
    </ul>

    <script>
        export default new Vue({
            name: '',
            data: function() {
                return {
                    list: [
                        {lable: 'one', id: 1},
                        {lable: 'two', id: 2},
                        {lable: 'three', id: 3},
                        {lable: 'four', id: 4},
                        {lable: 'five', id: 5},
                    ]
                }
            },
            method: {
                handleClick(id, event) {
                    console.log(id)
                }
            }
        })
    </script>
```

## 拓展

#### <a id="eventFlow" style="color: black;">事件流</a>

![event_flow](/assets/DOM_Event/event_flow.jpg)
capture 捕获阶段
target 目标阶段
bubbling 冒泡阶段
具体了解，去往[事件流](https://www.w3.org/TR/DOM-Level-3-Events/#event-flow)