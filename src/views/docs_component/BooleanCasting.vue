<template>
  <p>为了更贴近原生 Boolean attributes 的行为，声明为 boolean 类型的 props 有特别的类型转换规则。以带有如下生命的 MyComponent 组件为例：</p>
  <p>该组件可以被这样使用：</p>
  <!-- 等同于传入 :disabled="true" -->
  <MyComponent disabled />

  <!-- 等同于传入 :disabled="false" -->
  <MyComponent />
  <p>当一个 prop 被声明为允许多种类型时，Boolean 的转换规则也将被应用。然而，当同时允许 String 和 Boolean 时，有一种边缘情况——只有当 Boolean 出现在 String 之前时，Boolean 转换规则才适用：</p>
</template>

<script setup>
// disabled 将被转换为 true
defineProps({
  disabled: [Boolean, Number]
})

// disabled 将被转换为 true
defineProps({
  disabled: [Boolean, String]
})

// disabled 将被转换为 true
defineProps({
  disabled: [Number, Boolean]
})

// disabled 将被解析为空字符串 (disabled="")
defineProps({
  disabled: [String, Boolean]
})
</script>
