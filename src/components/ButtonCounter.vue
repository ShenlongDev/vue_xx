<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <button @click="count++">我是被点击{{ count }}遍。</button>
</template>
