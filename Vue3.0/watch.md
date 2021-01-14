# watch

watch API 完全等效于 2.x this.$watch （以及 watch 中相应的选项）。watch 需要侦听特定的数据源，并在回调函数中执行副作用。默认情况是懒执行的，也就是说仅在侦听的源变更时才执行回调。

* 对比 watchEffect，watch 允许我们：

* * 懒执行副作用；

  * 更明确哪些状态的改变会触发侦听器重新运行副作用；

  * 访问侦听状态变化前后的值。
* 侦听单个数据源

侦听器的数据源可以是一个拥有返回值的 getter 函数，也可以是 ref：

```
// 侦听一个 getter
const state = reactive({ count: 0 })
watch(
  () => state.count,
  (count, prevCount) => {
    /* ... */
  }
)
// 直接侦听一个 ref
const count = ref(0)
watch(count, (count, prevCount) => {
  /* ... */
})
```

* 侦听多个数据源

```
watch([fooRef, barRef], ([foo, bar], [prevFoo, prevBar]) => {
  /* ... */
})
```

* 与 watchEffect 共享的行为

watch 和 watchEffect 在停止侦听, 清除副作用 \(相应地 onInvalidate 会作为回调的第三个参数传入\)，副作用刷新时机 和 侦听器调试 等方面行为一致.

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



