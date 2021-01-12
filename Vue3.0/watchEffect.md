# watchEffect

### 官方解释

watchEffect官方的解释为”传入一个函数，并且立即执行，响应式追踪其依赖，并在其依赖变更时重新运行该函数。“

## 注册监听：

```
import {watchEffect} from 'vue' //导入api
const count = ref(0) //定义响应数据
watchEffect(() => console.log(count.value)) //注册监听函数
//打印出0
setTimeout(() => {
    count.value++
    //打印出1
},1000)
console.log("计时器外输出count.value", count.value); //打印出0
//执行顺序为watchedEffect中的console.log第一，计时器外的console.log第二，计时器执行后watchEffect监听到的console.log第三

```

## 注销监听：

默认情况下在”组件卸载“的时候停止监听，也可以显式地”调用返回值“以停止监听

```
const stop = watchEffect(() => {
    //需要监听的内容
})
//之后
stop()
```

## 清除副作用：

有时副作用函数会执行一些异步的副作用, 这些响应需要在其失效时清除（即完成之前状态已改变了）。所以侦听副作用传入的函数可以接收一个 onInvalidate 函数作入参, 用来注册清理失效时的回调。

当以下情况发生时，这个失效回调会被触发:

* 副作用即将重新执行时

* 侦听器被停止

```
const count = ref(0)
watchEffect(
  (onInvalidate) => {
    console.log(count.value, '副作用')
   const token =  setTimeout(() => {
      console.log(count.value, '副作用')
    }, 4000)
    onInvalidate(() => {
    // id 改变时 或 停止侦听时
    // 取消之前的异步操作
    token.cancel()
  })
  }
)
```

## 副作用刷新时机：

Vue 的响应式系统会缓存副作用函数，并异步地刷新它们，这样可以避免同一个 tick 中多个状态改变导致的不必要的重复调用。在核心的具体实现中, 组件的更新函数也是一个被侦听的副作用。当一个用户定义的副作用函数进入队列时, 会在所有的组件更新后执行

```
<template>
  <div>{{ count }}</div>
</template>
<script>
  export default {
    setup() {
      const count = ref(0)
      watchEffect(() => {
        console.log(count.value)
      })
      return {
        count,
      }
    },
  }
</script>
```

在这个例子中：

* count 会在初始运行时同步打印出来

* 更改 count 时，将在组件更新后执行副作用。

如果副作用需要同步或在组件更新之前重新运行，我们可以传递一个拥有 flush 属性的对象作为选项（默认为 'post'）：

```
// 同步运行
watchEffect(
  () => {
    /* ... */
  },
  {
    flush: 'sync',
  }
)
// 组件更新前执行
watchEffect(
  () => {
    /* ... */
  },
  {
    flush: 'pre',
  }
)
```

## 例子：

```
<template>
  <div>
    <h1>Hello Vue 3!</h1>
    {{name}}{{obj.sex}}
    <button @click="inc">Clicked {{ count }} times.</button>
  </div>
</template>

<script>
import { ref,reactive,computed,readonly,watchEffect } from 'vue'
export default {
  setup() {
    let count = ref(0)
    let res=1;
    let name = ref('jeff')
    let timer
    const obj=reactive({sex:'male'})
    const robj=readonly(obj); 
    let r=readonly('aa') //不具有只读的能力
    watchEffect((onInvalidate)=>{
      console.log(count.value);
      onInvalidate(()=>{
        console.log('清除');
        clearInterval(timer);
      })

    },  {
    onTrigger(e) {
      console.log(e);
    },
    onTrack(e)
    {
      console.log('triger');
      console.log(e)
    }
  })    
    const inc = () => {

      timer=setInterval(()=>{
        count.value++;
      },1000)

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
img {
  width: 200px;
}
h1 {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
```



