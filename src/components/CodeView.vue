<script setup>
defineProps(['content'])
</script>


<template>
  <div class="code-container">
    <pre>{{ content }}</pre>
  </div>
</template>


<style scoped>
.code-container {
  background: rgb(41, 45, 62);
  color: white;
  border-radius: 0.5rem;
  padding: 1rem 2rem;
  margin: 2rem -1rem;
}
</style>
