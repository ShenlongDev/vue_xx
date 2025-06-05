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
  <h3>绑定对象</h3>
  <p>:style支持绑定JavaScript对象值，对应的是HTML元素的style属性：</p>
  <div :style="{ color: activeColor, fontSize: fontSize + 'px' }">
    <p>尽管推荐使用camelCase，但：style也支持kebab-cased形式的CSS属性key（对应其CSS中的实际名称），例如：</p>
    <div :style="{ 'font-size': fontSize + 'px' }">我是kebab-case</div>
  </div>
  <p>直接绑定一个样式对象通常是一个好主意，这样可以使模板更加简洁</p>

  <div :style="sstyleObject">
    <p>同样的，如果样式对象需要更复杂的逻辑，也可以使用返回样式对象的计算属性。</p>
    <p>：style指令也可以和常规的 style attribute共存，就像：class。</p>
  </div>

  模板
  <h1 style="color: red" :style="'font-size: 1em'">hello</h1>
  这将被渲染为：
  <h1 style="color: red; font-size: 1em;">hello</h1>
</template>

<style scoped></style>
