<script setup>
import { createApp } from 'vue'
import ComponentProps from './views/docs_component/ComponentProps.vue'

const app = createApp({})

app.component('ComponentProps', ComponentProps)
</script>

<template>
  <ComponentProps />
</template>
