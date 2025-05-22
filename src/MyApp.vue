<script setup>
import { ref, reactive } from 'vue'

const books = reactive([ref('Vue 3 Guide')])
// 这里需要 .value
console.log(books[0].value)

const map = reactive(new Map([['count', ref(0)]]))
// 这里需要 .value
console.log(map.get('count').value)
</script>

<template>
  额外的ref解包细节
  <h1>作为reactive对象的属性</h1>
  <p>一个ref会在作为响应式对象的属性被访问或修改时自动解包。和换句话说，他的行为就像一个普通的属性：</p>

  <p>如果将一个新的ref赋值给一个关联了已有ref的属性，那么他会替换掉旧的ref：</p>

  <h1>数组和集合的注意事项</h1>
  <p>与reactive对象不同的是，当ref作为响应式数组或原生集合类型（如Map）中的元素被访问时，他不会被解包</p>
</template>

<style scoped></style>
