## Global API 的变化

## Global API 改为应用程序实例调用

vue2中很多全局api可以改变vue行为，比如Vue.component等。由此也引发了一系列问题：

* vue2没有app的概念，new Vue\(\)得到的根实例被作为app，这样的话所有创建的根实例是共享相同的全局配置，导致测试时会污染其他测试用例，使测试变得困难。
* 全局配置导致没有办法在单页面创建不同全局配置的多个app实例。

vue3中可以使用createApp返回app实例，由它暴露一系列全局api

```
import { createApp } from "vue";
const app = createApp({})
    .component('comp', { render: () => h('div', 'i am comp ') })
    .mount('#app')
```

列举如下：

| 2.x Global API | 3.x Instance API \(app\) |
| :--- | :--- |
| Vue.config | app.config |
| Vue.config.productionTip | removed |
| Vue.config.ignoredElements | app.config.isCustomElement |
| Vue.component | app.component |
| Vue.directive | app.directive |
| Vue.mixin | app.mixin |
| Vue.use | app.use |
| Vue.filter | removed |

TIP:

这些内容我在平时用的不算很多，具体列出在上表，有疑问的小伙伴可以自己查询一下官方文档

## Global and internal APIs 重构为可做摇树优化

在vue2中不少global-api是作为静态函数直接挂载在构造函数上的，例如Vue.nextTick\(\)，如果我们在代码中从未使用过他们，就会形成所谓的dead code，这类global-api造成的dead code无法使用webpack的tree-shaking排除掉，这样就导致打包完后的包会输出一些无用的废代码。

```
import Vue from 'vue'
Vue.nextTick() => {
    ...
})
```

vue3中做了相应的变化，将它们抽取成独立函数，这样打包工具的摇树优化可以将这些dead code排除掉。

```
import { nextTick } from 'vue'
nextTick(() => {
    ...
})
```

受影响的API：

* Vue.nextTick
* Vue.observable \(replace by Vue.reactive\)
* Vue.version
* Vue.compile \(only in full builds\)
* Vue.set \(only in compat builds\)
* Vue.delete \(only in compat builds\)



