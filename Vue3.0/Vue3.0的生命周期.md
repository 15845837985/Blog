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

因为 `setup` 是围绕 `beforeCreate` 和 `created` 生命周期钩子运行的，所以不需要显式地定义它们。换句话说，在这些钩子中编写的任何代码都应该直接在 `setup` 函数中编写,这些函数接受一个回调函数，当钩子被组件调用时将会被执行.

其中onRenderTracked和onRenderTriggered是vue3.0中新增加的生命周期函数，两个钩子函数都接收一个DebuggerEvent，与 watchEffect 参数选项中的 onTrack 和 onTrigger 类似：

        onRenderTracked\(\(e\)=&gt;{

          debugger //当一个 reactive对象属性或一个ref被追踪时触发

        }\)



        onRenderTriggered\(\(e\)=&gt;{

         debugger // 依赖项变更被触发时 检查哪个依赖性导致组件重新渲染

        }\)

结合下面这段代码进行分析：

```
<template>
  <div>
    <h1>Hello Vue 3!</h1>
    {{name}}{{obj.sex}}
    <button @click="inc">Clicked {{ count }} times.</button>
  </div>

</template>

<script>
import { ref,reactive,computed,watchEffect,watch,onMounted, onUpdated, onUnmounted,onRenderTracked,onRenderTriggered } from 'vue'

export default {
  setup() { //作用相当于vue2.x中的beforeCreate和created，在vue3.x中其他钩子函数需要在setup()内使用
    let count = ref(0)
    let count2=ref(2);
    let name = ref('vue 2.x')
    const obj=reactive({sex:'male'})
    const robj=readonly(obj); 

    onMounted(()=>{
      console.log('挂载后');
    })
    onRenderTracked((e)=>{
      console.log(e)
    })
    onRenderTriggered((e)=>{
      console.log(e);
    })

    const inc = () => {

       count.value++;
       name.value='vue 3.x'

    }

    return {
      count,
      inc,
      name, //在setup返回对象中自动解套
      obj
    }
  }
}
</script>

<style scoped>

h1 {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
```



