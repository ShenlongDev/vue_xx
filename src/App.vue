<script setup>
import { createApp } from 'vue'
import ComponentRegister from './feature/ComponentRegister.vue'
import ComponentBasic from './ComponentBasic.vue'

const app = createApp({})

app
// .component(
//   // 组件的名字
//   'ComponentTest',
//   // 组件的实现
//   {
//   template: `
//     <p>这是全局注册实例</p>
//   `
// })
.component('ComponentRegister', ComponentRegister)
.component('ComponentBasic', ComponentBasic)
</script>

<template>
  <ComponentRegister />
  <ComponentBasic />
</template>
