<script setup>
import { ref } from 'vue'
const isActive = ref(true)
const hasError = ref(false)
</script>

<template>
  <h1>类与样式绑定</h1>
  <h2>绑定 HTML class</h2>
  <h3>绑定对象</h3>
  <p>我们可以给 :class (v-bind:class 的缩写) 传递一个对象来动态切换 class：</p>
  <div class="static" :class="{ active: isActive, 'text-danger': hasError }">
    <p>这里的语法表示active是否存在取决于数据属性isActive的真假值。</p>
    <p>你可以在对象中写多个字段来操作多个class。</p>
    <p>此外，：class指令也可以和一般的 class attribute共存。</p>
    <p>举例来说</p>
  </div>
</template>

<style scoped></style>
