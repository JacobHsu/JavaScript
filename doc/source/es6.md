title: ECMAScript 6 
---

[ECMAScript 6 入门](http://es6.ruanyifeng.com/)

## Module 的加载实现

浏览器允许脚本异步加载，下面就是两种异步加载的语法。

```js
<script src="path/to/myModule.js" defer></script>
<script src="path/to/myModule.js" async></script>
```
上面代码中，`<script>`标签打开`defer`或`async`属性，脚本就会异步加载。渲染引擎遇到这一行命令，就会开始下载外部脚本，但不会等它下载和执行  

### 加载规则
`<script type="module" src="./foo.js"></script>`  

```js
<script type="module">
  import './index.js';
</script>
```
 
