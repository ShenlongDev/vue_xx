<script setup>
</script>

<template>
  <h1>事件处理</h1>

  <h2>监听事件</h2>
  <p>
    我们可以使用 v-on 指令 (简写为 @) 来监听 DOM 事件，并在事件触发时执行对应的 JavaScript。
    用法：v-on:click="handler" 或 @click="handler"。
    事件处理器 (handler) 的值可以是：
    <b>1.内联事件处理器</b>：事件被触发时执行的内联 JavaScript 语句 (与 onclick 类似)。
    <b>2.方法事件处理器</b>：一个指向组件上定义的方法的属性名或是路径。
  </p>
</template>
