# Fragments & Emits Component Option

## Fragments:

vue3中组件可以拥有多个根

```
 <template>
  <header>...</header>
  <main v-bind="$attrs">...</main>
  <footer>...</footer>
</template>
```

## Emits Component Option:

vue3中组件发送的自定义事件需要定义在emits选项中

优点：

* 更好的指示组件的工作方式
* 对象形式事件校验
* 避免和原生事件重名导致事件触发两次，如click

```
<template>
  <div @click="$emit('click')">
      自定义事件
  </div>
</template>

<script>
export default {
    emits: ['click']
}
</script>
```



