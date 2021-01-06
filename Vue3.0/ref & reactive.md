# ref & reactive

## ref:

接受一个参数值并返回一个响应式且可改变的 ref 对象。ref 对象拥有一个指向内部值的单一属性 value。

```
const count = ref(0)
console.log(count.value) // 0
count.value++
console.log(count.value) // 1
```

## reactive:

接收一个普通对象然后返回该普通对象的响应式代理。等同于vue 2.x 的 Vue.observable\(\)。

```
const obj = reactive({ count: 0 })
```

## TIP:

* ref常用于基本类型，reactive用于引用类型。如果ref传入对象，其实内部会自动变为reactive。
* 当 ref 作为渲染上下文的属性返回（即在setup\(\) 返回的对象中）并在模板中使用时，它会自动解套，无需在模板内额外书写 .value。

```
<template>
  <div>{{ count }}</div>
</template>
<script>
  export default {
    setup() {
      return {
        const count = ref(0)
        count: count, // 而不是 count.value
      }
    },
  }
</script>
```

* 当 ref 作为 reactive 对象的 property 被访问或修改时，也将自动解套 value 值，其行为类似普通属性。

```
const count = ref(0)
const state = reactive({
  count,
})
console.log(state.count) // 0
state.count = 1
console.log(count.value) // 1
```

* 注意当嵌套在 reactive Object 中时，ref 才会解套。从 Array 或者 Map 等原生集合类中访问 ref 时，不会自动解套。

```
const arr = reactive([ref(0)])
// 这里需要 .value
console.log(arr[0].value)
const map = reactive(new Map([['foo', ref(0)]]))
// 这里需要 .value
console.log(map.get('foo').value)
```



