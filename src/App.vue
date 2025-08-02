<script setup>
import { createApp } from 'vue'
import PropValidation from './views/docs_component/PropValidation.vue'

const app = createApp({})

app.component('PropValidation', PropValidation)
</script>

<template>
  <PropValidation />
</template>
