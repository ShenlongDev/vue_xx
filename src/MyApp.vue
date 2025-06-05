<script setup>
import { ref } from 'vue'
const activeColor = ref('red')
const fontSize = ref(30)
</script>

<template>
  <h1>类与样式绑定</h1>
  <h2>绑定内联样式</h2>
  <h3>绑定对象</h3>
  <p>:style支持绑定JavaScript对象值，对应的是HTML元素的style属性：</p>
  <div :style="{ color: activeColor, fontSize: fontSize + 'px' }">
    <p>尽管推荐使用camelCase，但：style也支持kebab-cased形式的CSS属性key（对应其CSS中的实际名称），例如：</p>
    <div :style="{ 'font-size': fontSize + 'px' }">我是kebab-case</div>
  </div>
</template>

<style scoped></style>
