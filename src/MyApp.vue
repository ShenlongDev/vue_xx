<script setup>
  const number = 100
</script>

<template>
  使用JavaScript表达式
  至此，我们进在模板中绑定了一些简单的属性名。
  但是vue实际上在所有的数据绑定中都支持完整的JavaScript表达式：

  <span>{{ number + 1 }}</span>

  这些表达式都会被作为Javascript，以当前组件实例为作用域解析举行。
  在Vue模板内，JavaScript表达式可以被使用在如下场景上：
  在文本插值中（双大括号）
  在任何Vue指令（以v-开头的特殊attribute）attribute的值中

  仅支持表达式
  每个绑定仅支持单一表达式，也就是一段能够被求求值的JavaScript代码。
  一个简单的判断方法是是否可以合法地写在return后面。
  因此，下面的例子都是无效的

  调用函数
  可以在绑定的表达式中使用一个组件暴露的方法
</template>

<style scoped>
  
</style>
