<script setup>
// defineProps(['title'])
const props = defineProps(['title'])
</script>

<template>
  <div class="blog-post">
    <h4>{{ props.title }}</h4>
    <button @click="$emit('enlarge-text')">放大文字</button>
  </div>
</template>
