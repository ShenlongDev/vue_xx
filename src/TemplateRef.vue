<script setup>
import { useTemplateRef, onMounted, watchEffect } from 'vue';

// 第一个参数必须与模板中的 ref 值匹配
const input = useTemplateRef('my-input')

onMounted(() => {
  input.value.focus()
})

watchEffect(() => {
  if (input.value) {
    input.value.focus()
  } else {
    // 此时还未挂载，或此元素已经被卸载（例如通过 v-if 控制）
  }
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
  在使用 TypeScript 时，Vue 的 IDE 支持和 vue-tsc 将根据匹配的 ref attribute 所用的元素或组件自动推断 input.value 的类型。
  —— 3.5以前的用法
  注意，你只可以在组件挂载后才能访问模板引用。
  如果你想在模板中的表达式上访问 input，你初次渲染时会是 null。
  这是因为在初次渲染前这个元素还不存在呢！
  如果你需要侦听一个模板引用 ref 的变化，确保考虑到其值为 null 的情况：
  也可参考：为模板引用标注类型

  <h2>组件上的 ref</h2>
  这一小节假设你已了解组件的相关知识，或者你也可以先跳过这里，之后在回来看。
</template>
