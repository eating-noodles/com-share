---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS (experimental)
css: unocss
---

# 前端分享

VueJS设计与实现

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space to start<carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---


# 目录
- 🧑‍💻 **早些年的前端 && 现代前端**
  - 命令式和声明式
  - 运行时和编译时
- 👏 **VueJs**
  - 渲染器的作用
  - 编译器的作用
- 🤹 **实现响应式**
  - 基本思路
  - 边界问题
<br>
<br>


<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# 早些年的前端
一个HTML页面的基本组成

<div grid="~ cols-2 gap-4">
<div>


```html {all|1-9,20|10-14|15-19|all}
<!DOCTYPE html>
<html>
<head>
  <title>Hello World</title>
</head>
<body>
  <h1>Hello World</h1>
  <button @onclick="hello()"></button>
</body>
<script>
  function hello() {
    alert('Hello World');
  }
</script>
<style>
  h1 {
    color: red;
  }
</style>
</html>
```


</div>
<div>
运行效果:
<div bg-stone-3 p-5>
<!-- ./components/Hello.vue -->
<Hello></Hello>
</div>

|     |     |
| --- | --- |
| HTML | 页面的骨架 |
| JAVASCRIPT | 逻辑的实现 |
| CSS | 样式的呈现 |
</div>
</div>

---

# 实现一个简单的功能

``` html
<div id="app"></div>
```

现在有上面的代码片段，期望：
1. 给标签设置内容为"Hello World";
2. 当我们点击这个`div`标签时，可以弹出一个提示框，提示内容是`Hello World`。

原生JS要怎么实现？

<div v-click>

1. 根据id获取到元素
2. 使用HTML元素提供的Api可以为其设置内容
3. 为其绑定点击事件及点击时的逻辑

</div>
---

# 实现一个简单的功能


<div grid="~ cols-2 gap-4">
<div>

原生js代码实现：

```javascript
const div = document.getElementById('app');

div.innerHTML = 'Hello World';
div.addEventListener('click', function() {
  alert('Hello World');
}
```
<p v-click="1">
如果使用Vue，实现方式是什么样的？

</p>

<div v-click="3">

- 代码的实现详细的描述了我们想要的功能
- 代码本身就是"做事的过程",符合我们的逻辑直觉
- 更加的关注**过程**
</div>

<div v-click="5">
<p>

## 命令式

</p>
</div>
</div>
<div v-click="2">

Vue代码实现：

``` html 

<div @click="() => alert('Hello World')">
  Hello World
</div>



```
<p color-white> vue</p>
<div v-click="4">

- 代码描述了一个**结果**
- 具体实现的"过程",代码中并没有体现
- Vue帮我们封装了过程

</div>

<div v-click="5">
<p>

## 声明式

</p>
</div>
</div>
</div>

<style>
h2 {
  background-color: #000000;
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# 现代前端框架

VueJs、React等框架

|     |     |   |
| --- | --- | --- |
| 一个网站的基本功能  | 早些年前端开发 | 现代js框架 |
| 拥有一个或者多个页面 | 几个页面即对应几个HTML | 只有一个HTML页面 |
| 多个页面之间的跳转 | 页面之间的跳转即HTML之间的跳转 | 页面组件的呈现以及跳转控制由js控制 |

<p mt-10 v-click="1">

- 业务和需求简单时，无伤大雅，甚至静态页面足矣。
- 随着业务日益复杂，前端需求和代码也变得日益复杂。
- 前端逐渐发展起来
  - less,sass等
  - react、vue、svelte等及其衍生技术
  - node, webpack, rollup等
  - ...
</p>

---

# 编译时和运行时

``` html
<div>
  <span>hello world</span>
</div>
```
观察上面的代码片段，能否抽象为一个类或者某种数据结构？


<div grid="~ cols-2 gap-4">
<div v-click="1">

``` typescript
class HELLO {
  tag: string;
  children: HELLO[] || string;
}

const basic = {
  tag: '',
  children: [],
  // children: '',
}
```

</div>
<div v-click="2">

``` javascript
const obj = {
  tag: 'div',
  children: [
    {
      tag: 'span',
      children: 'hello world'
    }
  ]
}


```
</div>
</div>

<p v-click="3">

- 根据`html`片段, 我们抽象出树状的数据结构。
- 反过来想，那如果给我们树状结构的对象，我们是不是可以实现一个`Render`函数去生成`html`片段?

</p>
---

# 实现一个Render函数

<div grid="~ cols-2 gap-4">
<div>

``` javascript
function Render(obj, root) {
  const el = document.createElement(obj.tag);
  if (typeof obj.children === 'string') {
    const text = document.createTextNode(obj.children);
    el.appendChild(text);
  } else if (obj.children) {
    obj.children.forEach(child => {
      Render(child, el);
    });
  }
  root.appendChild(el);
}

```
``` javascript
// 实际使用
const obj = {
  tag: 'div',
  children: [{
      tag: 'span',
      children: 'hello world'
    }]
}
Render(obj, document.body);
```
</div>
<div>

实现思路：
1. `document.createElement`可以根据元素类型创建元素
2. `document.createTextNode`可以根据文本内容创建文本节点
3. `el.appendChild`可以将子节点添加到父节点中
4. 已知对象的数据格式，`tag`标明`html`元素类型，可根据tag来创建元素
5. `children`标明子节点的数据,但是有两种类型
  * 当其为string时，表示文本节点，创建文字节点添加
  * 当其为数组时，表示子节点的数组，递归调用`Render`函数


</div>
</div>
---

# 实现一个Render函数

<p>
我们刚刚编写的`Render`函数，其实可以算是一个微型的**纯运行时**的框架。
</p>
思考它的不足，可以发现：
<p v-click="1">

- 我们每次使用的时候，都必须手动去写树形结构的数据对象，这样是不是太麻烦了？
- 这样写出来的代码，并不直观
</p>
<p v-click="2">
能不能支持类似于HTML标签的方式描述树形结构的数据对象呢？
</p>

---

# 编译时

``` javascript
  const html  = `
  <div>
    <span>hello world</span>
  </div>
  `;

  const obj = Compiler(html);

  Render(obj, document.body);
```
<p>
上面的代码片段给出了我们理想中的使用场景
</p>
<p v-click="1">

`Compiler`是我们要实现的函数
- 入参：`html`模板字符串
- 出参：前文中我们定义的树状结构的对象
</p>
<p v-click="1">

至此, 我们实现了一个**运行时** + **编译时**的框架; 
而且我们的`Render`函数和`Compiler`可以分别使用，也可以一起使用。我们可以在用户运行代码时，**运行时编译**;也可以构建时就先进行编译，运行的时候就无须编译了，这对性能提升来说是非常有效的。
</p>

---

#  编译时

<div>

<p v-click="1">有没有人有疑问？</p>
<p v-click="2">刚才我们做的事情，不就是把`html`转成了树状对象；然后又把树状对象转成了`html`吗？</p>
<p v-click="2">这不是在套娃吗？</p>

</div>

--- 

# VueJs

给大家看一个简单的VueJs文件：

``` javascript
<template>
  <div>
    hello world
  </div>
</template>

<script>
export default {
  data () {/*... */},
  methods: {
    /*... */
  },
}
</script>
<style></style>
```
<p v-click="1">
一个vue文件，开发中一般就是一个组件(页面)，内容上分为三部分。
</p>

<p v-click="2">浏览器是不认识vue文件的，最后都要转成`html`,`js`,`css`的</p>
<p v-click="3">就是靠的渲染器和编译器</p>

---

# 虚拟DOM和渲染函数

<div grid="~ cols-2 gap-4">
<div v-click="1">

<p>
前面总结出来的树状结构的数据对象:
</p>

``` javascript
const obj = {
  tag: 'div',
  children: [
    {
      tag: 'span',
      children: 'hello world'
    }
  ]
}




```
<p v-click="2">
我们用js对象来描述了UI，而这种js对象描述UI的方式就是所谓的`虚拟DOM`
</p>
</div>
<div v-click="3">
<p>
vue中组件还有一种写法，就是使用渲染函数`h`
</p>

``` javascript
import { h } from 'vue'

export default {
  data() {
    return {
      msg: 'hello world'
    }
  },
  render() {
    return h('div', this.msg)
  }
}
```

<p v-click="4">这种方式就是使用`虚拟DOM`来描述UI。其中的`h`函数是用来辅助创建`虚拟DOM`的工具函数。</p>

<p v-click="5">
组件的渲染函数：用来描述UI的函数，返回值是`虚拟DOM`。
</p>
</div>
</div>
---

# 渲染器

<div>
前面实现的渲染方法:
</div>

``` javascript
function Render(obj, root) {
  const el = document.createElement(obj.tag);
  if (typeof obj.children === 'string') {
    const text = document.createTextNode(obj.children);
    el.appendChild(text);
  } else if (obj.children) {
    obj.children.forEach(child => {
      Render(child, el);
    });
  }
  root.appendChild(el);
}

```
<p v-click="1">

这个方法接收`虚拟DOM`,生成`真实DOM`并挂载。这就是**渲染器**的作用。
</p>
<p v-click="2">
如果按照我们上面的定义，它其实不应该叫渲染函数。它是一个功能不算完善的渲染器。
</p>

<p v-click="3">
这里的渲染器只是在创建节点，其实渲染器还有一个更为关键的作用，那就是更新节点，当vnode(虚拟DOM对象)发生改变时，它需要精确的找到vnode的变更点并且只更新变更的内容。
</p>

---

# 渲染器的简单实现

``` javascript
function renderer(vnode, container) {
  const el = document.createElement(vnode.tag);
  for(const key in vnode.props) {
    if(/^on/.test(key)){
      el.addEventListener(
        key.substr(2).toLowerCase(),
        vnode.props[key]
      )
    }
  }

  if(typeof vnode.children === 'string') {
    const text = document.createTextNode(vnode.children);
    el.appendChild(text);
  } else if(Array.isArray(vnode.children)) {
    vnode.children.forEach(child => {
      renderer(child, el);
    });
  }

  container.appendChild(el);
}
```

---

# 对比两种vue文件的写法


<div grid="~ cols-2 gap-4">
<div>

<p>模板写法</p>

``` javascript
<template>
  <div>
    hello world
  </div>
</template>

<script>
export default {
  data () {/*... */},
  methods: {/*... */},
}
</script>
```
</div>

<div>

<p>渲染函数写法</p>

``` javascript
import { h } from 'vue'

export default {
  data() {
    return {
      /*... */
    }
  },
  render() {
    return h('div', 'hello world')
  }
}

```
</div>
</div>

<p v-click="1">相比模板写法，渲染函数写法少了第一部分的模板标签(类似于html的标签)，同时，渲染函数多了`render`函数。</p>

<p v-click="2">

在vue中，最后都是需要`渲染器`来渲染UI，而渲染函数是来为`渲染器`生成`虚拟DOM`的。"左边写法"中的模板最后也要转换成渲染函数，而**编译器**就是将模板编译成渲染函数的。</p>
