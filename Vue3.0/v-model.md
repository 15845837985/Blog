# v-model

vue3中将model选项和v-bind的sync修饰符被移除，统一为v-model参数形式

```
<div id="app">
    <h3>{{data}}</h3>
    <comp v-model="data"></comp>
    <!--等效于-->
    <comp :modelValue="data" @update:modelValue="data=$event"></comp>
</div>
```

    app.component('comp', {
      template:`
        <div @click="$emit('update:modelValue', 'new value')">
          i an comp, {{modelValue}}
        </div>
        `,
        props: ['modelValue']
    })

子组件中的model选项移除

