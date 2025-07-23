<script setup>
import { createApp } from 'vue'
import ComponentRegister from './feature/ComponentRegister.vue'

const app = createApp({})

app.component('ComponentRegister', ComponentRegister)
</script>

<template>
  <ComponentRegister />
</template>
