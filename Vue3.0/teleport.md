# teleport——传送门

## 什么是teleport

teleport是一种能够将模板移动到DOM中Vue.app之外其他位置的技术，我们姑且称其为传送门

## 使用场景

类似modals，toast这类的元素，如果我们嵌套在Vue的某个组件内部，处理嵌套组件的定位、z-index和样式就会变得很困难，但如果将它完全与Vue应用的DOM完全剥离，管理起来会方便很多。

另外，像modals，toast这类的元素需要使用Vue组件的状态（data或者props）的值，我们便可以在组件的逻辑位置写模板代码，这样就可以使用组建的data或props，然后在Vue应用的范围外渲染它。

## 例子：

```
<template>
  <div>
    <button @click="modalOpen = true">弹出一个模态窗口</button>

    <teleport to="body">
      <div v-if="modalOpen" class="modal">
        <div>
          这是一个弹窗 我的父元素是body
          <button @click="modalOpen = false">关闭</button>
        </div>
      </div>
    </teleport>
  </div>
</template>

<script>
export default {
  data() {
    return {
      modalOpen: false,
    };
  },
};
</script>

<style>...
```

在上面例子中我单独封装了一个ModalButton组件，这个组件控制一个模态窗口的弹出，通过控制modalOpen来控制窗口的开启关闭，在teleport组件中，通过to属性，指定该组件渲染位置在body下，也可以通过to属性指向要添加组件的标签的id来决定组件渲染的位置。通过v-if控制窗口的显示。

##### TIP：

看大家说teleport的功能有些类似React中的Portals，React中的Portals提供了一种将子节点渲染到存在于父组件以外的DOM节点的方案。可惜我对React了解较少，了解多的小伙伴可以结合理解





