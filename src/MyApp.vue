<script setup>
  const seen = true
  const url = 'https://blabla...'
  const doSth = () => {
    alert('干的漂亮，你在听我的事件')
  }
</script>

<template>
  指令Directives
  指令是带有v-前缀的特殊attribute。
  Vue提供了许多内置指令， 包括上面我们所介绍的v-bind和v-html。
  指令attribute的期望值为一个JavaScript表达式（除了少数几个例外，及之后要讨论到的）
  一个指令的任务是在其表达式的值变化是响应式地更新DOM。
  以v-if为例：
  <a :href="url"><p v-if="seen">Now you see me</p></a>
  这里，v-if指令急用钱表达式seeen 的值的真移除/插入这个p元素。
  参数Arguments
  某些指令会需要一个参数，在指令名后通过一个冒号隔开做标识
  这里href就是一个参数，他告诉v-bind指令将表达式url的值绑定元组的hrefattribute上。在简写中，参数前的一切都会被缩略为一个：字符
  另一个例子是v-
  <a v-on:click="doSth">i你好，我是监听事件的</a>
</template>

<style scoped>
  
</style>
