<template>
  <h1>Props</h1>
  <h2>传递 prop 的细节</h2>
  <h3>Prop 名字格式</h3>
  <h3>静态 vs. 动态 Props</h3>
  <h3>传递不同的值类型</h3>
  <p>在上述的两个例子中，我们只传入了字符串值，但实际上任何类型的值都可以作为 props 的值被传递。</p>
  <h4>Number</h4>
  <h4>Boolean</h4>
  <h4>Array</h4>
  <h4>Object</h4>
  <h3>使用一个对象绑定多个 prop</h3>
  <p>如果你想要将一个对象的所有属性当做 props 传入，你可以使用没有参数的 v-bind，机制使用 v-bind 而非：prop-name。例如，这里有一个 post 对象：</p>
  <post-blog v-bind="post"></post-blog>
</template>

<script setup>
import PostBlog from '@/components/PostBlog.vue'

const post = {
  title: 'This is the first post',
  likes: 5003,
  commentIds: [234, 266, 273],
  author: {
    name: 'Veronica',
    company: 'Veridian Dynamics'
  }
}
</script>
