<template>
  <h1>Props</h1>
  <h2>响应式 Props 解构</h2>
  <p>Vue 的响应系统基于属性访问跟踪状态的使用情况。例如，在计算属性或侦听器中访问 props.foo 时，foo 属性将被跟踪为依赖项。</p>
  <p>因此，在一下代码的情况下：</p>
  <p> 3.4 及以下版本，foo 是一个实际的常量，永远不会改变。在 3.5 及以上版本，当在同一个 script setup 代码块中访问由 defineProps 解构的变量时，Vue 编译器会自动在前面添加 props.。因此，上面的代码等同于以下代码：</p>
  <p>此外，你可以使用 JavaScript 原生的默认值语法声明 Props 默认值。这在使用基于类型的 props 声明时特别有用。</p>
  <p>如果你希望在 IDE 中在解构的 props 和普通变量之间有更多视觉上的区分，Vue 的 VSCode 扩展提供了一个设置来启用解构 props 的内联提示。</p>
</template>

<script setup>
import { watchEffect } from 'vue'
// const { foo } = defineProps(['foo'])

// watchEffect(() => {
//   // 在 3.5 之前只运行一次
//   // 在 3.5+ 中在 "foo" prop 变化时重新执行
//   console.log(foo)
// })
const props = defineProps(['foo'])

watchEffect(() => {
  // `foo` 由编译器转换为 `props.foo`
  console.log(props.foo)
})
</script>
