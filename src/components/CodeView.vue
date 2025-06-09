<script>
import { defineProps } from 'vue'
const props = defineProps(['content'])
</script>


<template>
  <div class="code-container">
    <pre>{{ props.content }}</pre>
  </div>
</template>


<style>
.code-container {
  background: black;
  color: white;
}
</style>
