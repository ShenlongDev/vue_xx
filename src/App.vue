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
import ComponentBasic from './ComponentBasic.vue';
import ComponentRegister from './feature/ComponentRegister.vue'

export default {
  components: {
    ComponentRegister: ComponentRegister,
    ComponentBasic,
  }
}
</script>

<template>
  <ComponentRegister />
  <ComponentBasic />
</template>
