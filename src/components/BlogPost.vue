<!-- BlogPost.vue -->
<script setup>
defineProps(['title'])
const emit = defineEmits(['enlarge-text'])

emit('enlarge-text')
</script>

<!-- BlogPost.vue, 省略了 <script> -->
<template>
  <div class="blog-post">
    <h4>{{ title }}</h4>
    <button @click="$emit('enlarge-text')">Enlarge text</button>
  </div>
</template>
