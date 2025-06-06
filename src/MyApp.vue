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
  <h3>自动前缀</h3>
  <p>我们还可以给：style绑定一个包含多个样式对象的数组。</p>
  <p>这些对象会被合并后渲染到同意元素上：</p>
  <div :style="[baseStyles, overridingStyles]"></div>
  <p>当你在 :style 中使用了需要浏览器特殊前缀的 CSS 属性时，Vue 会自动为他们加上相应的前缀。Vue 是在运行时检查该属性是否支持在当前浏览器中使用。如果浏览器不支持某个属性，那么将尝试加上各个浏览器特殊前缀，以找到哪一个是被支持的。</p>
</template>

<style scoped></style>
