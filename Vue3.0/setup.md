# setup\(\)

setup功能是新的组件选项。它是组件内部暴露出所有的属性和方法的统一API。

## 调用时机：

创建组件实例，然后初始化 props ，紧接着就调用setup 函数。从生命周期钩子的视角来看，它会在 beforeCreate 钩子之前被调用

## 结合模板使用：

如果 setup 返回一个对象，则对象的属性将会被合并到组件模板的渲染上下文

```
<template>
  <div>
    <h1>Something about setup()</h1>
    <div>书名：{{ book.title}} 阅读人数：{{ readersNumber}}</div>
    <button @click="add">已读</button>
  </div>

</template>

<script>
import { toRefs, ref, reactive } from 'vue'

export default {
  setup() {
    const readersNumber = ref(0)
    const book = reactive({ title: 'Vue 3 Guide'})
    const add = () => {
      readersNumber.value++
    }
    return {
      readersNumber,
      book,
      add
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

可从上面例子中看到，从setup 返回的refs在模板中访问时是自动解套的，因此不应在模板中使用 xxx.value。

setup还可以返回一个渲染函数，给渲染函数可以直接使用在同一作用域中声明的响应式状态：

```
<script>
import { toRefs, ref, reactive, h } from 'vue'

export default {
  setup() {
    const readersNumber = ref(0)
    const book = reactive({ title: 'Vue 3 Guide'})
    return () => h('div', [readersNumber.value,book.title])
  }
}
</script>
```

## setup\(\)参数：

### 1.**props**

第一个参数接受一个响应式的props，这个props指向的是外部的props。如果你没有定义props选项，setup中的第一个参数将为undifined。

##### 注意：1.不要在子组件中修改props；如果你尝试修改，将会给你警告甚至报错。

##### 2.不要解构props。解构的props会失去响应性。

### 2.**上下文对象**

第二个参数提供了一个上下文对象，从原来 2.x 中 this 选择性地暴露了一些 property。

