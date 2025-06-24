<script setup>
defineProps(['content']);
</script>

<template>
  <span class="en-letters">{{ content }}</span>
</template>

<style scoped>
.en-letters {
  background-color: #eee;
  color: #213547;
  padding: 0.25rem 0.5rem;
  margin: 0 0.5rem;
  border-radius: 0.25rem;
}
</style>
