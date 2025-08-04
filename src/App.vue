<script setup>
import { createApp } from 'vue'
import BooleanCasting from './views/docs_component/BooleanCasting.vue'

const app = createApp({})

app.component('BooleanCasting', BooleanCasting)
</script>

<template>
  <BooleanCasting />
</template>
