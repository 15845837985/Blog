# Global API 改为应用程序实例调用

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



