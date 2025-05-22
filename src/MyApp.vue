<script setup>
import { ref, reactive } from 'vue'

const count = ref(0)
const state = reactive({
  count
})

console.log(state.count)
state.count = 1
console.log(count.value)

const otherCount = ref(2)
state.count = otherCount
console.log(state.count)
state.count++
console.log(otherCount.value)

console.log(count.value)
</script>

<template>
  额外的ref解包细节
  <h1>作为reactive对象的属性</h1>
  <p>一个ref会在作为响应式对象的属性被访问或修改时自动解包。和换句话说，他的行为就像一个普通的属性：</p>

  <p>如果将一个新的ref赋值给一个关联了已有ref的属性，那么他会替换掉旧的ref：</p>
</template>

<style scoped></style>
