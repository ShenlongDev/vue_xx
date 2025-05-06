<script setup>
  const seen = true
</script>

<template>
  指令Directives
  指令是带有v-前缀的特殊attribute。
  Vue提供了许多内置指令， 包括上面我们所介绍的v-bind和v-html。
  指令attribute的期望值为一个JavaScript表达式（除了少数几个例外，及之后要讨论到的）
  一个指令的任务是在其表达式的值变化是响应式地更新DOM。
  以v-if为例：
  <p v-if="seen">Now you see me</p>
  这里，v-if指令急用钱表达式seeen 的值的真移除/插入这个p元素。

</template>

<style scoped>
  
</style>
