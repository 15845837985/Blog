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

## 例子：

    <template>
      <p>{{ counter }}</p>
      <p>{{ doubleCounter }}</p>
      <p>{{ msg }}</p>
      <p ref="desc"></p>
    </template>

    <script>
    import { computed, onUnmounted, reactive, onMounted, ref, toRefs, watch} from "vue";
    export default {
      setup() {
        const { counter, doubleCounter } = useCounter();
        const msg = ref("seconds");
        const desc = ref(null);
        watch(counter, (val, oldVal) => {
          const p = desc.value;
          p.textContent = `counter from ${oldVal} to ${val}`;
        });

        return { counter, doubleCounter, msg, desc };
      },
    };
    function useCounter() {
      const data = reactive({
        counter: 1,
        doubleCounter: computed(() => data.counter * 2),
      });

      let timer;

      onMounted(() => {
        timer = setInterval(() => {
          data.counter++;
        }, 1000);
      });

      onUnmounted(() => {
        clearInterval(timer);
      });

      return toRefs(data);
    }
    </script>



