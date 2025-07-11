<script setup>
import { ref } from 'vue'

const cnt = ref(0)
</script>

<template>
  <button @click="cnt++">This button clicked {{ cnt }} times.</button>
</template>
