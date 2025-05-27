<script setup>
import { ref, computed } from 'vue'

const firstName = ref('John')
const lastName = ref('Doe')

const fullName = computed({
  // getter
  get() {
    return firstName.value + ' ' + lastName.value
  },
  // setter
  set(newValue) {
    // 注意：我们这里使用的是解构赋值语法
    [firstName.value, lastName.value] = newValue.split(' ')
  }
})
</script>

<template>
  <h1>计算属性</h1>
  <h2>可写计算属性</h2>
  <p>计算属性默认是只读的。当你尝试修改一个计算属性时，你会收到一个运行时警告。</p>
  <p>旨在某些特殊场景中你可能才需要用到“可写”的属性，你可以通过同时提供getter和setter来创建：</p>
  <p>现在当你在运行fullName.value='John Doe'时，setter会被调用而first Name和lastName会随之更新。</p>
</template>

<style scoped></style>
