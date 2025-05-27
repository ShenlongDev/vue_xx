<script setup>
import { ref, computed } from 'vue'
const count = ref(2)

const alwaysSmall = computed((previous) => {
  if (count.value <= 3) {
    return count.value
  }

  return previous
})

const alwaysSmall1 = computed({
  get(previous) {
    if (count.value <= 3) {
      return count.value
    }

    return previous
  },
  set(newValue) {
    count.value = newValue * 2
  }
})
</script>

<template>
  <h1>计算属性</h1>
  <h2>获取上一个值</h2>
  <p>仅3.4+支持</p>
  <p>如果需要，可以通过访问计算属性的Getter的第一个参数来获取计算属性返回的上一个值。</p>
  <p>如果你正在使用可写的计算属性的话</p>
</template>

<style scoped></style>
