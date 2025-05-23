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
</script>

<template>
  <h1>计算属性</h1>
  <h2>基础示例</h2>
  <p>模板中的表达式虽然方便，但也只能用来做简单的操作。如果在模板中写太多逻辑，会让模板变得臃肿，难以维护。</p>
  <p>比如说，我们有这样一个嵌套数组的对象：</p>
  <p>我们想根据 author 是否已有一些书籍来展示不同的信息</p>
  <p>Has published Books: </p>
  <span>{{ author.books.length > 0 ? 'yes' : 'no' }}</span>

  <p>这里的模板看起来有些复杂。我们必须认真看好一会儿才能明白他的计算依赖于author.books。</p>
  <p>更重要的是，如果我们在模板中需要不止一次这样的计算，我们可不想将这这样的代码在模板里重复好多遍。</p>
  <p>因此我们推荐你使用计算属性来描述以来响应式状态的复杂逻辑。这是重构后的示例</p>
  <p>Has published Books: </p>
  <span>{{ publishedBooksMessage }}</span>
</template>

<style scoped></style>
