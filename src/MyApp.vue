<script setup>
import { reactive, computed } from 'vue'

const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

// 一个计算属性 ref
const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No'
})

// 组件中
function calculatedBooksMessage() {
  return author.books.length > 0 ? 'Yes' : 'No'
}

const now = computed(() => Date.now())
</script>

<template>
  <h1>计算属性</h1>
  <h2>计算属性缓存 vs 方法</h2>
  <p>你可能注意到我们在表达式中想这样调用一个函数也会获得和计算属性相同的结果：</p>
  <p>{{ calculatedBooksMessage() }}</p>
  <p>若我们将同样的函数定义为一个方法而不是计算属性，两种方式在结果上确实是完全相同的，然而</p>
  <p>不同之处在于计算属性值会给予其响应式以来被缓存。</p>
  <p>一个计算属性仅会在其响应式依赖更新时才重新计算。这意味着只要author.books不改变，无论多少次访问</p>
  <p>publishedBooksMessage都会立即返回先前的计算结果，而不用重复举行getter函数。</p>
  <p>这也解释了为什么下面的计算属性永远不会更新，因为Date.now()并不是一个响应式依赖</p>
  <p>相比之下，方法调用总是会在重渲染发生时再次举行函数。</p>
  <p>为什么需要缓存呢？想象一下我们有一个非常耗性能的计算属性list，需要循环一个巨大的数组并作许多计算逻辑，并且可能也有其他计算属性依赖于list。</p>
  <p>没有缓存的话，，我们会重复举行非常多次list的getter，然而这实际上没有必要！</p>
  <p>如果你确定不需要缓存，那么也可以使用方法调用。</p>
</template>

<style scoped></style>
