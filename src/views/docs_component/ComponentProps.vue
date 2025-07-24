<template>
  <h1>Props</h1>
  <h2>Props 声明</h2>
  <p>一个组件需要显式声明它所接受的 props，这样 Vue 才能知道外部传入的哪些是 props，哪些是透传 attribute。</p>
  <p>在使用 script setup 的单文件组件中，props可以使用 defineProps() 宏来声明。</p>
  <p>在没有使用 script setup 的组件中，props 可以用 props 选项来声明：</p>
  <p>注意传递给 defineProps() 的参数和提供给 props 选项的值是相同的，两种声明方式背后其实使用的都是 props 选项。</p>
  <p>除了声明字符串数组来声明 props 外，还可以使用对象的形式：</p>
  <p>对于以对象形式声明的每个属性， key 是 prop 的名称，而值则是该 prop 预期类型的构造函数。比如，如果要求一个 prop 的值是 number 类型，则可使用 number 构造函数作为其声明的值。</p>
  <p>对象形式的 props 声明不仅可以一定程度上作为组件的文档，而是如果其他开发者在使用你的组件时传递了错误的类型，也会在浏览器控制台中抛出警告。我们将在本章节稍后进一步讨论有关 prop 校验的更多细节。</p>
  <p>如果你正在搭配 TypeScript 使用 script setup, 也可以使用类型标注来声明 props:</p>
</template>

<script setup lang="ts">
defineProps<{
  title?: string
  likes?: number
}>()
</script>
