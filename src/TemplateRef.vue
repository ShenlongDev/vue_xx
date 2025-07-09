<script setup>
import { useTemplateRef, onMounted } from 'vue';

// 第一个参数必须与模板中的 ref 值匹配
const input = useTemplateRef('my-input')

onMounted(() => {
  input.value.focus()
})
</script>

<template>
  <h1>模板引用</h1>
  虽然 Vue 的声明性渲染模型为你抽象了大部分对 DOM 的直接操作，
  但在某些情况下，我们仍然需要直接访问底层 DOM 元素。
  要实现这一点，我们可以使用特殊的 ref 属性：
  <input ref="input">
  ref 是一个特殊的 attribute，和 v-for 章节中提到的 key 类似。
  它允许我们在一个特定的 DOM 元素或子组件实例被挂载后，获得对他的直接引用。
  这可能很有用，比如说在组件挂载时将焦点设置一个 input 元素上，或在一个元素上初始化一个第三方库。

  <h2>访问模板引用</h2>
  要在组合式 API 中获取引用，我们可以使用辅助函数 useTemplateRef():
  <input ref="my-input">
</template>
