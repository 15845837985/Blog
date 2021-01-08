# ref & reactive

## ref:

接受一个参数值并返回一个响应式且可改变的 ref 对象。ref 对象拥有一个指向内部值的单一属性 value。

```
import { ref } from 'vue'
const count = ref(0)
console.log(count.value) // 0
count.value++
console.log(count.value) // 1
```

## reactive:

接收一个普通对象然后返回该普通对象的响应式代理。等同于vue 2.x 的 Vue.observable\(\)。

```
import { reactive } from 'vue'
const obj = reactive({ count: 0 })
```

## TIP:

ref常用于基本类型，reactive用于引用类型。如果ref传入对象，其实内部会自动变为reactive。

## ref解套（展开）：

当 ref 作为渲染上下文的属性返回（即在setup\(\) 返回的对象中）并在模板中使用时，它会自动解套，无需在模板内额外书写 .value。

```
<template>
  <div>{{ count }}</div>
  <button @click="add">点我</button>
</template>
<script>
import {ref} from "vue";

  export default {
    setup() {
        const count = ref(0)
        const add = () => {
            count.value++
        }
      return {
         count,
         add
      }
    },
  }
</script>
```

## 访问响应式对象：

当 ref 作为 reactive 对象的 property 被访问或修改时，也将自动解套 value 值，其行为类似普通属性。

```
import { reactive, toRef, ref } from "vue";

export default {
  setup() {
    const count = ref(0)
    const OtherCount = ref(2)
    const state = reactive({
      count
    });
    console.log(state.count); //0
    console.log(count.value); //0
    state.count = 1;
    console.log(state.count); //1
    console.log(count.value); //1
    state.count = OtherCount; //如果有新的ref赋值给现有ref的property，将会替换旧的ref
    console.log(state.count); //2
    console.log(count.value); //1
  },
};
</script>
```

注意当嵌套在 reactive Object 中时，ref 才会解套。从 Array 或者 Map 等原生集合类中访问 ref 时，不会自动解套。

```
const arr = reactive([ref(0)])
// 这里需要 .value
console.log(arr[0].value)
const map = reactive(new Map([['foo', ref(0)]]))
// 这里需要 .value
console.log(map.get('foo').value)
```

## 响应式状态解构：

当使用大型reactive对象的一些property时，可能想使用ES6解构来获取想要的property，如果直接使用ES6中的解构，解构的property的响应性都会丢失，此时需要将响应式对象转换为一组ref，这些ref会保留与源对象的响应式关联

```
<script>
import { reactive, toRefs, ref } from "vue";
const book = reactive({
    author: 'Vue Team',
    year: '2020',
    title: 'ref & reactive',
    description: 'You are reading this book right now',
    price: 'free'
})

//let {author , title} = book    直接解构author和title的响应性会丢失
let {author , title} = toRefs(book)
title.value = 'Vue 3 Guid'
console.log(book.title);
console.log(book.author);
</script>
```



