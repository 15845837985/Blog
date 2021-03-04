# v-if与v-for同时使用

当select下拉框需要v-for循环数据且有部分选项需要控制隐藏，这就需要同时使用v-for与v-if，在el-option中同时使用v-if和v-for会报错，那么解决方法不如将el-option外面套一个template

例子

```
<el-select>
    <template v-for="item in selectOptions>
        <el-option
          v-if="!['1','2','3'].includes(item.code)"
          :key="item.xx"
          :label="item.xx"
          :value="item.xx"
        />
    </template>
</el-select>
```



