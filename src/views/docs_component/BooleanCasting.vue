<template>
  <p>为了更贴近原生 Boolean attributes 的行为，声明为 boolean 类型的 props 有特别的类型转换规则。以带有如下生命的 MyComponent 组件为例：</p>
  <p>该组件可以被这样使用：</p>
  <!-- 等同于传入 :disabled="true" -->
  <MyComponent disabled />

  <!-- 等同于传入 :disabled="false" -->
  <MyComponent />
</template>

<script setup>
defineProps({
  disabled: Boolean
})
</script>
