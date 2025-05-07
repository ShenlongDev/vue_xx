<script setup>
import { reactive } from 'vue'

const state = reactive({ count: 0 })
</script>

<template>
  <button @click="state.count++">
    {{ state.count }}
  </button>

  还有另一种声明响应式状态的方式，及使用reactive()API。
  与将内布置包装在特殊对象中的ref不同，reactive()将使对象本身具有响应性。
  响应式对象是JS代理，其行为就和普通对象一样。
  不同的是Vue能够拦截对响应式对象所有属性的访问和修改，一遍进行以来追踪和触发更新。
  reactive() 将深层地转换对象：当访问嵌套对象时，它们也会被 reactive() 包装。当 ref 的值是一个对象时，ref() 也会在内部调用它。与浅层 ref 类似，这里也有一个 shallowReactive() API 可以选择退出深层响应性。
</template>

<style scoped></style>
