# 第一节 Vue3.0的生命周期

## 一、vue2.0到vue3.0中生命周期的变化

> vue2.0：    -----------------------------------------------------------------    vue3.0

```
beforecreate  -------------------------------------------------------------  setup()

created  ---------------------------------------------------------------------  setup()

beforeMount  -------------------------------------------------------------  onBeforeMount  

mounted  --------------------------------------------------------------------  onMounted  

beforeUpdate  -------------------------------------------------------------  onBeforeUpdate  

updated  ----------------------------------------------------------------------  onUpdated  

beforeDestroy  ------------------------------------------------------------  onBeforeDestroy

destroyed  ------------------------------------------------------------------  onDestroyed  

errorCaptured  ------------------------------------------------------------  onErrorCaptured
```

简单来说:

* vue3.0中取消了vue2.0中的beforecreate和created两个生命周期，同时新增了一个setup\(\)
* 可以通过生命周期钩子前面加上“on"来访问组件的生命周期钩子
* 可以在setup\(\)内部调用生命周期钩子

| setup\(\)内部调用生命周期钩子如下表： |
| :--- |


| 选项式API | Hook inside setup |
| :--- | :--- |
| beforeCreate | Not needed\* |
| created | Not needed\* |
| beforeMount | onBeforeMounted |
| mounted | onMounted |
| beforeUpdate | onBeforeUpdate |
| updated | onUpdated |
| beforeUnmount | onBeforeUnmount |
| umounted | onUnmounted |
| errorCaptured | onErrorCaptured |
| renderTracked | onRenderTracked |
| renderTriggered | onRenderTriggered |

TIP

因为 `setup` 是围绕 `beforeCreate` 和 `created` 生命周期钩子运行的，所以不需要显式地定义它们。换句话说，在这些钩子中编写的任何代码都应该直接在 `setup` 函数中编写。（上面表格中后五个钩子我接触较少，如果有误欢迎补充）

这些函数接受一个回调函数，当钩子被组件调用时将会被执行:

```

// MyBook.vue
 
export default {
  setup() {
    // mounted
    onMounted(() => {
      console.log('Component is mounted!')
    })
  }
}
```





