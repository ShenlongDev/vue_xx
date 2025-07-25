<template>
  <h1>Props</h1>
  <h2>响应式 Props 解构</h2>
  <p>Vue 的响应系统基于属性访问跟踪状态的使用情况。例如，在计算属性或侦听器中访问 props.foo 时，foo 属性将被跟踪为依赖项。</p>
  <p>因此，在一下代码的情况下：</p>
</template>

<script setup>
import { watchEffect } from 'vue'
const { foo } = defineProps(['foo'])

watchEffect(() => {
  // 在 3.5 之前只运行一次
  // 在 3.5+ 中在 "foo" prop 变化时重新执行
  console.log(foo)
})
</script>
