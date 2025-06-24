<script setup>
defineProps(['heading'])
</script>


<template>
  <div class="heading-container">
    <span class="heading">{{ heading }}</span>
  </div>
</template>


<style scoped>
.heading-container {
  display: inline-block;
  padding: 0.5rem 1rem;
  margin: 1rem;
  border-radius: 0.25rem;
  background-color: lightgray;
  color: #213547;
}

.heading {
  font-size: 1.5rem;
  font-weight: bold;
}
</style>
