<script setup>
defineProps(['content'])
</script>


<template>
  <div class="code-container">
    <pre>{{ content }}</pre>
  </div>
</template>


<style>
.code-container {
  background: black;
  color: white;
}
</style>
