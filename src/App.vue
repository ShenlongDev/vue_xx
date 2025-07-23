<!-- <script setup>
import { createApp } from 'vue'
import ComponentRegister from './feature/ComponentRegister.vue'

const app = createApp({})

app.component('ComponentRegister', ComponentRegister)
</script>

<template>
  <ComponentRegister />
</template> -->
<script>
import ComponentRegister from './feature/ComponentRegister.vue'

export default {
  components: {
    ComponentRegister
  }
}
</script>

<template>
  <ComponentRegister />
</template>
