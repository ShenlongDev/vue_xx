<script setup>
import { ref } from 'vue'
const activeClass = ref('active')
const errorClass = ref('text-danger')
const isActive = ref(true)
</script>

<template>
  <h1>类与样式绑定</h1>
  <h2>绑定 HTML class</h2>
  <h3>绑定数组</h3>
  <p>我们剋以给：class绑定一个数组来渲染多个CSS class:</p>
  <div :class="[activeClass, errorClass]"></div>

  <div class="active text-danger">渲染的结果时：</div>

  <div :class="[isActive ? activeClass : '', errorClass]">
    如果你也想在数组中有条件地渲染某个class，你可以使用三元表达式：
  </div>

  <div :class="[{ [activeClass]: isActive }, errorClass ]">
    errorClass会一直存在， 但activeClass之会在isActive为真时才存在。
    然而，这可能在有多个以来条件的class时会有些冗长。因此也可以在数组中嵌套对象。
  </div>
</template>

<style scoped></style>
