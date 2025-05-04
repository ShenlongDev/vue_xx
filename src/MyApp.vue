<script setup>
  const msg = 'Hello, Vue3!'
  const rawHtml = '<span style="color: red">This should be red.</span>'
</script>

<template>
  <p>{{ msg }}</p>
  <p>Using text interpolation: {{ rawHtml }}</p>
  <p>Using v-html directive: <span v-html="rawHtml"></span></p>
</template>

<style scoped>
  p {
    font-size: 40px;
  }
</style>
