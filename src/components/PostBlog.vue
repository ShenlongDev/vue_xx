<script setup>
defineProps(['title'])
const emit = defineEmits(['enlarge-text', 'reduce-text'])
const handleEnlarge = () => {
  emit('enlarge-text')
}
</script>

<template>
  <div class="blog-post">
    <h4>{{ title }}</h4>
    <button @click="handleEnlarge">放大文字</button>
    <button @click="$emit('reduce-text')">放小文字</button>
  </div>
</template>
