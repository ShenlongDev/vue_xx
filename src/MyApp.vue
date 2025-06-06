<script setup>
import { ref, reactive } from 'vue'
const activeColor = ref('red')
const fontSize = ref(30)
const sstyleObject = reactive({
  color: 'red',
  fontSize: '30px'
})
</script>

<template>
  <h1>类与样式绑定</h1>
  <h2>绑定内联样式</h2>
  <h3>绑定数组</h3>
  <p>我们还可以给：style绑定一个包含多个样式对象的数组。</p>
  <p>这些对象会被合并后渲染到同意元素上：</p>
  <div :style="[baseStyles, overridingStyles]"></div>
</template>

<style scoped></style>
