<script setup></script>

<template>
  <h1>类与样式绑定</h1>
  <h2>绑定内联样式</h2>
  <h3>样式多值</h3>
  <p>你可以对一个样式属性提供多个（不同前缀的）值，举例来说</p>
  <div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
  <p>数组金辉渲染浏览器支持的最后一个值。</p>
  <p>在这个实例中，在支持不需要特别前缀的浏览器中都会渲染为 display： flex。</p>
</template>

<style scoped></style>
