# computed

computed和vue2.x版本保持一致，支持getter和setter

## 用法：

传入一个 getter 函数，返回一个默认不可手动修改的 ref 对象。

```
const count = ref(1);
const plusOne = computed(() => count.value + 1);
console.log(plusOne.value); //2
plusOne.value++; //不可手动修改
console.log(plusOne.value); //依旧是2
```

或者传入一个拥有 get 和 set 函数的对象，创建一个可手动修改的计算状态。

```
const count = ref(1)
const plusOne = computed({
  get: () => count.value + 1,
  set: (val) => {
    count.value = val - 1
  },
})
plusOne.value = 1
console.log(count.value) // 0
```



