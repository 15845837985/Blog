# 第一节 Vue3.0的生命周期

## 一、vue2.0到vue3.0中生命周期的变化

> vue2.0：    -----------------------------------------------------------------    vue3.0

```
beforecreate  -------------------------------------  setup()

created  ------------------------------------------  setup()

beforeMount  --------------------------------------  onBeforeMount  

mounted  ------------------------------------------  onMounted  

beforeUpdate  -------------------------------------  onBeforeUpdate  

updated  ------------------------------------------  onUpdated  

beforeDestroy  ------------------------------------  onBeforeDestroy

destroyed  ----------------------------------------  onDestroyed  

errorCaptured  ------------------------------------  onErrorCaptured
```

### 简单来说:

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

### TIP：

因为 `setup` 是围绕 `beforeCreate` 和 `created` 生命周期钩子运行的，所以不需要显式地定义它们。换句话说，在这些钩子中编写的任何代码都应该直接在 `setup` 函数中编写,这些函数接受一个回调函数，当钩子被组件调用时将会被执行.

其中onRenderTracked和onRenderTriggered是vue3.0中新增加的生命周期函数，两个钩子函数都接收一个DebuggerEvent，与 watchEffect 参数选项中的 onTrack 和 onTrigger 类似：

```
    onRenderTracked((e)=>{

      debugger //当一个 reactive对象属性或一个ref被追踪时触发

    })

    onRenderTriggered((e)=>{

     debugger // 依赖项变更被触发时 检查哪个依赖性导致组件重新渲染

    })
```

### 基本例子：

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
  setup() { //作用相当于vue2.x中的beforeCreate和created
    let count = ref(0)
    let count2=ref(2);
    let name = ref('vue 2.x')
    const obj=reactive({sex:'male'}) 
    const inc = () => {

       count.value++;
       name.value='vue 3.x'

    }
    onBeforeMounted(()=>{
      console.log('挂载前')
    })
    onMounted(()=>{
      console.log('挂载后');
    })
    onBeforeUpdate(()=>{
      console.log('更新前')
    })
    onUpdated(()=>{
      console.log('更新后')
    })
    onRenderTracked((e)=>{
      console.log(e)
    })
    onRenderTriggered((e)=>{
      console.log(e);
    })


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

### setup\(\):

setup功能是新的组件选项。它是组件内部暴露出所有的属性和方法的统一API。

### 调用时机：

创建组件实例，然后初始化 props ，紧接着就调用setup 函数。从生命周期钩子的视角来看，它会在 beforeCreate 钩子之前被调用

### 使用方法：

如果 setup 返回一个对象，则对象的属性将会被合并到组件模板的渲染上下文

```
<template>
  <div>{{ count }} {{ object.foo }}</div>
</template>
<script>
  import { ref, reactive } from 'vue'
  export default {
    setup() {
      const count = ref(0)
      const object = reactive({ foo: 'bar' })
      // 暴露给模板
      return {
        count,
        object,
      }
    },
  }
</script>
```

### setup\(\)参数：

#### 1.**props**

第一个参数接受一个响应式的props，这个props指向的是外部的props。如果你没有定义props选项，setup中的第一个参数将为undifined。

##### 注意：1.不要在子组件中修改props；如果你尝试修改，将会给你警告甚至报错。

##### 2.不要解构props。解构的props会失去响应性。

#### 2.**上下文对象**

第二个参数提供了一个上下文对象，从原来 2.x 中 this 选择性地暴露了一些 property。

### TIP：

由于vue3.x向下兼容vue2.x,所以一个vue文件中你可以同时写两个版本的东西。

```
import { reactive, computed, watch, onMounted } from 'vue'
export default {
  name: 'HelloWorld',
  props: {
    count: Number,
  },
  data () {
    return {
      msg: "我是vue2.x中的this"
    }
  },
  methods: {
    test () {
      console.log(this.msg)
    }
  },
  mounted () {
    console.log('vue2.x mounted')
  },
  // eslint-disable-next-line no-unused-vars
  setup (props, val) {
    console.log(this, 'this') // undefined
    onMounted(() => {
      console.log('vue3.x mounted')
    })
    return {
      ...props
    }
  }
}
```

#### 1.vue2.x和vue3.x的生命周期函数同时存在时的执行顺序

由于这个例子中写了mounted（2.x）,在setup函数中又写了onMounted（3.x），那么在两个版本的生命周期函数同时存在时他们的执行顺序应该是怎样的便自然而然成为了首要问题。经过测试得到结论，setup\(\)中的钩子函数先执行。因为创建组件实例初始化 props 之后紧接着就调用setup 函数，所以setup\(\) 在解析 vue2.x 选项前就被调用了。

#### 2.在vue2.x选项中中定义在this上的变量，在setup上可以通过this访问吗？可以重复定义吗？可以return吗？

首先在setup中的this将不再指向vue,而是undefined;所以在setup函数内部自然无法访问到vue实例上的this。

setup内部定义的变量和外表的变量并无冲突；

但是如果你要将其return 暴露给template,那么就会产生冲突。

